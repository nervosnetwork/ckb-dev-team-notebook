# Postmortem

A project post-mortem is a process used to identify the causes of a project failure (or significant business-impairing downtime), and how to prevent them in the future. This is different from a retrospective, in which both positive and negative things are reviewed for a project.

## A Postmortem Reference

<https://github.com/envoyproxy/envoy/blob/main/security/postmortems/cve-2019-9900.md>

```markdown
# Security postmortem for CVE-2019-9900, CVE-2019-9901

## Incident date(s)

2019-02-18 - 2019-04-05

## Authors

@htuch

## Status

Final

## Summary

Two independent vulnerabilities related to a mismatch between the information used for request
matching and routing were discovered in February/March 2019, leading to the potential ability for an
attacker to bypass access control checks and route table intent. Since these issues had similar
attack vectors and were discovered within the same embargo window, the issues were grouped and
resolved (mostly) privately by Envoy and Istio fix teams, resulting in the Envoy 1.9.1 security
release issued on 2019-04-05.

This was the first time in which the Envoy security release process was followed and provided a
learning opportunity to refine the process, originally borrowed from the Kubernetes project, to
Envoy's requirements. While the issues were upgraded from medium to high criticality during the fix
process, they were limited in impact to a subset of users and specific configuration patterns. This
postmortem captures the issues encountered during the fix process and provides actionable next
steps.

## CVE issue(s)

* https://github.com/envoyproxy/envoy/issues/6434
* https://github.com/envoyproxy/envoy/issues/6435

## Root Causes

CVE-2019-9900 resulted from Envoy assuming that its codec libraries (http-parser, nghttp2) followed
RFC 7230 and would reject any header value with an embedded NUL character. Unfortunately,
http-parser did not do this due to an optimization in header value processing
(https://github.com/nodejs/http-parser/issues/468, https://github.com/nodejs/http-parser/pull/469).
In addition, Envoy viewed header strings with a mixture of `c_str()` and `string_view`, allowing the
possibility of inconsistent views between checks and resulting action. A combination of a buggy
external dependency and problematic use of C string views led to this vulnerability.

CVE-2019-9901 resulted from two distinct views of the role of a proxy in path handling. On the one
hand, Envoy was considered a data forwarding engine for HTTP requests that did not need to perform
path normalization, with this concern left to client and backend. However, at the same time, Envoy
was being used in applications where it intermediated on requests for access control purposes (e.g.
RBAC, `ext_authz`) and performed path matching against policy. Especially in the presence of a
backend that itself normalizes, this access control role required that path normalization be applied
in the proxy.

## Resolution

CVE-2019-9900 was reported by Envoy maintainer @htuch on 2019-03-10 to
envoy-security@googlegroups.com. After some discussion, it was agreed that this warranted invoking
the security release process. The issue was mitigated in the Envoy private security repository by
@htuch and the Envoy security fix team. A single patch
(https://github.com/envoyproxy/envoy/commit/b155af75fad7861e941b5939dc001abf581c9203) was required
to workaround the http-parser behavior. In addition, both tests and fuzzers were
created to validate the behavior when NULs were introduced anywhere in an HTTP/1 or HTTP/2 request
(https://github.com/envoyproxy/envoy/commit/1e61a3f95f2c4d9ac1e54feae8693cee7906e2eb). Manual code
inspection was also performed in nghttp2 to verify the absence of vulnerability. While doing so, a
non-security related bug was discovered (https://github.com/nghttp2/nghttp2/issues/1331).

Shortly after discovery of CVE-2019-9900, the http-parser issue was reported to the Node.js security
working group at security@nodejs.org, since http-parser lives under the umbrella of the Node.js
project. The full vulnerability was described and the Envoy security team proposed working with
Node.js PST. As there was no reply, we proceeded independently. Unfortunately, it appears that the
Node.js security WG never received the e-mail, due to the reliance of Node.js on HackerOne to gate
incoming issues and a problematic e-mail forwarding chain
(https://github.com/nodejs/security-wg/issues/454#issuecomment-481919759). We have since filed a
HackerOne issue with the original report e-mail.

CVE-2019-9901 was privately disclosed to the Istio security team by an external researcher on
2019-02-18 and accidentally publicly disclosed in part in
https://github.com/envoyproxy/envoy/issues/6008 on 2019-03-13. Once the severity of this was
realized via offline discussion between the Envoy security team and the PR authors, we moved to a
private fix process in conjunction with CVE-2019-9900, targeting the 1.9.1 release. The Google Istio
security and networking teams led the efforts to fix this vulnerability in Envoy's private security
repository. The workaround implementation of path normalization borrowed from Chromium's URL
library, adapted and minified for the Envoy context. The follow patches were
produced:
* https://github.com/envoyproxy/envoy/commit/c22cfd2c483fc26534382a0b6835f45264bb137a
* https://github.com/envoyproxy/envoy/commit/7ed6d2187df94c4cb96f7dccb8643bf764af2ccb

In both cases, the Envoy security team considered the issues of medium criticality (CVSS 6.5)
initially, since it was thought that the attack complexity was high, requiring special circumstances
to apply. As we continued discussion with Istio and Google teams, it became apparent that the
exploits were trivial to automate and we upgraded to high criticality (CVSS 8.3), due to the lower
attack complexity.

A 1.9.1 security release was initially targeted for 2019-04-02 and announced on 2019-03-22. An
e-mail was sent to the Envoy private distributor list sharing CVE details.

After private discussions with a distributor on 2019-03-28, who expressed concern over the very
short (3 working day) distance between fix patch availability and release, the Envoy security team
decided to delay the 1.9.1 release until 2019-04-05. This provided 1 week for distributors to
prepare their software for the security release date.

Fix patches were shared with the private distributor list late on 2019-03-28.

During the fix process, two distributors reached out to us to request the ability to stage in
publicly accessible locations binary images with the fixes applied. While technically this would
violate embargo, we decided to allow this due to a lack of a clear alternative; Envoy's sidecar
use cases and reliance on Docker for distribution, where images are generally staged on public hubs,
did not lend itself to opaque rollout.

## Detection

The underlying issue behind CVE-2019-9900 was first noticed via fuzzers when an explicit `ASSERT`
check for embedded NULs was added in #6170. The following issue was tripped by
`h1_capture_fuzz_test`:
https://bugs.chromium.org/p/oss-fuzz/issues/detail?id=13613. Some experiments with `netcat`, `tcpdump`
and an Envoy binary demonstrated that it was viable to at least bypass header suffix matches via
this mechanism.

CVE-2019-9901 was reported by an external researcher (Erlend Oftedal) to the Istio security team.

## Action Items

* https://github.com/envoyproxy/envoy/issues?utf8=%E2%9C%93&q=is%3Aissue+%22Action+item+for+CVE-2019-9900%22+
* https://github.com/envoyproxy/envoy/issues?utf8=%E2%9C%93&q=is%3Aissue+%22Action+item+for+CVE-2019-9901%22+

## Lessons Learned

### What went well

* Fix patches were available within 2 weeks of vulnerability disclosure. The
  changes were localized and relatively clean.

### What went wrong

* The Envoy private distributor list was initially almost empty. We sent out an
  e-mail to remind distributors to sign up on 2019-03-14 and the list is now O(10).

* The security impact of https://github.com/envoyproxy/envoy/issues/6008
  was not caught by Envoy until this was brought to our attention ~20 days after
  the issue was first pushed. Ideally such issues should be routed to
  envoy-security@googlegroups.com first in the future and Envoy
  reviewers/maintainers should keep an eye out for inadvertent security
  disclosures through public channels. In addition, an earlier issue
  https://github.com/envoyproxy/envoy/issues/2956 was opened a year previous, but was not tagged as
  being security sensitive.

* Applicants for the private distributor list were turned down based on
  membership criteria that was adopted from k8s. This is now being revisited in
  https://github.com/envoyproxy/envoy/issues/6586.

* Distributors were only provided 3 days from candidate fix patch availability
  until public release at first. While this was extended to 1 week, even this
  might be too little. This is now being codified in
  https://github.com/envoyproxy/envoy/issues/6587.

* The Chromium URL library was forked, minified and adapted to Envoy. This was
  expedient but not a maintainable long term solution, see
  https://github.com/envoyproxy/envoy/issues/6588.

* Only coarse grained control over path normalization was provided, since this
  was expedient and mitigated the vulnerability. We should provide finer grained
  controls, see https://github.com/envoyproxy/envoy/issues/6589.

* Our report to the Node.js security working group was lost due to
  https://github.com/nodejs/security-wg/issues/454#issuecomment-481919759.
  We should avoid this happening Envoy-side, see https://github.com/envoyproxy/envoy/issues/6590.
  More generally, we should err on the side of reaching out over more channels
  in the future, since it's unclear how effective any given disclosure channel
  is.

* The security release day (2019-04-05) was Friday PDT. We should pick a
  globally friendly day-of-week, e.g. Tue-Thu, for security releases.

* Nginx already had a CVE for path normalization
  (https://www.rapid7.com/db/vulnerabilities/nginx-cve-2009-3898) similar to
  CVE-2019-9901, but we did not know this until after the fact. We should audit
  CVEs for similar class software, see
  https://github.com/envoyproxy/envoy/issues/6592.

* A distributor reached out to the security team for permission to perform
  silent binary rollouts as discussed above. While in principle our relaxation
  of the embargo policy applied to all distributors, an e-mail was not sent to
  the list. This resulted in confusion when a second distributor observed this
  rollout. We should ensure going forward that any policy relaxation during CVE
  handling is clearly communicated across the board.

* Public, albeit silent, staging of Docker images before the public security
  release date was a necessary pragmatic tradeoff. We need to refine the
  security release process to deal with this explicitly, see
  https://github.com/envoyproxy/envoy/issues/6593.

* The security release forced `envoy-dev:latest` back to the 1.9.1 release
  branch. This should be fixed, see
  https://github.com/envoyproxy/envoy/issues/6595.

* There was a window of ~50 minutes between the release tagging of the Envoy
  1.9.1 branch and availability of Docker images. Ideally we shrink this to
  allow users to upgrade faster. See
  https://github.com/envoyproxy/envoy/issues/6596.

* The CVE-2019-9901 fix required either control plane or runtime changes. This
  orchestration was not well suited to all deployment environments, so some
  distributions, e.g. Istio, applied additional patches to enable at compile
  time. Ideally we support control plane, runtime and CLI or compile-time fix
  opt-in abilities.

### Where we got lucky

* The defects were not critical (by CVSS scoring and intuition) and (mostly)
  privately disclosed. This provided an opportunity to exercise and refine the
  Envoy security release process.

* Huffman and HPACK in general frustrates HTTP/2 testing and fuzzing for security
  properties. We had no effective fuzzing or testing for this previously as a
  result, we were lucky that the scope of CVE-2019-9900 was limited to HTTP/1.1.

* CVE-2019-9900 was only discovered as a result of additional `ASSERT`s added to
  verify a property that Envoy developers were certain held. Fuzzing alone had
  not previously caught this.

* Distributors were able to execute their own security releases within the 1
  week provided from patch availability. Anecdotally, this involved effort
  beyond that which we should expect normally to manage an Envoy fix.

* No known instances reported of pre-release embargo breakage due to silent
  public staging of Docker images.

## Timeline

All times US/Pacific

2019-02-18:
* [CVE-2019-9901] Path normalization issue was reported to Istio security team at vulnerabilities@discuss.istio.io.

2019-02-19:
* [CVE-2019-9901] https://github.com/envoyproxy/envoy/issues/6008 was opened. This was not the first Envoy report of
  missing path normalization (see https://github.com/envoyproxy/envoy/issues/2956). Neither issue
  mentioned the security basis and Envoy reviewers speculated on the potential for path traversal
  attacks.

2019-03-08:
* [CVE-2019-9900] oss-fuzz reports https://bugs.chromium.org/p/oss-fuzz/issues/detail?id=13613 under embargo.

2019-03-10:
* [CVE-2019-9900] E-mail thread on envoy-security@googlegroups.com regarding the
  potential effects of this bugs. While it was unclear whether there would be
  impact beyond some narrow circumstances, agreement was reached to start the
  security release process. Analysis began to determine the extent of impact on
  HTTP/2 and Envoy's code base was audited.

2019-03-11:
* [CVE-2019-9901] https://github.com/envoyproxy/envoy/pull/6258 was opened to address
  https://github.com/envoyproxy/envoy/issues/6008.

2019-03-13:
* [CVE-2019-9901] https://github.com/envoyproxy/envoy/pull/6258 was closed after offline discussions
  between Envoy security team and the author, once the Envoy security team became aware of the
  potential severity in the Istio setup (in particular with RBAC and Mixer in play).

2019-03-14:
* [CVE-2019-9900] Finding were presented to envoy-security@. A fix plan was
  agreed upon and a candidate fix PR was shared with the team by e-mail. At this
  point, no private fix repository existed.
* [CVE-2019-9901] The Istio fix leads initiated private work on a fix patch.
  Since it was likely that this would land within the 1.9.1 release
  window for CVE-2019-9900, CVE-2019-9901 was also scheduled for the release.
* [Announcement](https://groups.google.com/forum/#!topic/envoy-announce/dEOLqAiaSUI) sent to remind
  distributors to join cncf-envoy-distributors-announce@lists.cncf.io.

2019-03-20:
* CVEs were requested from MITRE for both issues.
* Draft fix PRs for CVE-2019-9900 and CVE-2019-9901 were shared on private Envoy
  security repository. Reviews and further development occurred over the
  following week.

2019-03-22:
* 11:20 1.9.1 security release for the two vulnerabilities was
  [announced](https://groups.google.com/d/msg/envoy-announce/6fwGB2TxB74/dKeURAdfAgAJ).
* 11:24 CVE summary details shared with cncf-envoy-distributors-announce@lists.cncf.io.

2019-03-28:
* Envoy security team met with a distributor to discuss their concerns over the lack of time between
  patch availability and the release date. We agreed that three days was insufficient and agreed to
  extend to a week.
* 13:53 A delay of the 1.9.1 release until 2019-04-05 was
  [announced](https://groups.google.com/d/msg/envoy-announce/6fwGB2TxB74/Pe3PPFbPBAAJ).
* 20:07 Candidate fix patches for both CVE shared with
  cncf-envoy-distributors-announce@lists.cncf.io.

2019-03-29:
* Envoy security team was contacted by a distributor regarding the permissibility of silently
  staging binary images in public locations in advance of the security release due to a lack of
  viable alternatives. The Envoy security team agreed that there was no better alternative and
  provided an exemption.

2019-04-02:
* 08:15 The increase of severity from medium to high was
  [announced](https://groups.google.com/d/msg/envoy-announce/6fwGB2TxB74/qiDEgclFBgAJ).
  This followed several days of offline discussion between Istio and Envoy teams
  on Istio's independent assessment of the issues as high severity, and a better
  awareness of how to score. What was missing was the intuition that a
  vulnerability can be high severity even if it only affects a rather limited
  number of users.

2019-04-04:
* 15:41 The Envoy main branch was frozen to prepare for the security release. PRs were rebased
  against master and prepared for the release push.
* 18:33 Envoy security team was contacted by a distributor who had noticed public visibility of
  binary images with the fix patch by other vendors. After discussion, we agreed on a general
  exemption for these CVEs to the embargo policy for binary images with some constraints.
* 19:18 cncf-envoy-distributors-announce@lists.cncf.io was e-mailed to clarify position on staging
  of binary images on public sites prior to the release date. A narrow set of circumstances under
  which this was permissible were outlined.

2019-04-05:
* 10:00 - 10:05 The [v1.9.1](https://github.com/envoyproxy/envoy/tree/v1.9.1) release branch was
  pushed and the 1.9.1 releaes was tagged. This started the Docker build process for the release.
  The same PRs were pushed to master.
* 10:05 The Envoy 1.9.1 security release was
  [announced](https://groups.google.com/forum/?utm_medium=email&utm_source=footer#!topic/envoy-announce/VoHfnDqZiAM).
* 10:57 The v1.9.1 image was available at https://hub.docker.com/r/envoyproxy/envoy/tags.

## Supporting information
```
