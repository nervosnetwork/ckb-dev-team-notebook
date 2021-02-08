---
created: 2020-08-21
updated: 2020-08-27
author: ian yang
---

# CKB Transactions Management Guideline

[![hackmd-github-sync-badge](https://hackmd.io/lA8KVycmQU6oqWjPzQZNYA/badge)](https://hackmd.io/lA8KVycmQU6oqWjPzQZNYA)

UTXO transactions management is hard because they may be stuck in or even dropped from the CKB node transactions pool when the fee is too low.

This guideline is for any transactions generator which wants to trace the transaction status before finally confirmed in the chain.

## Transaction States

The transaction lifecycle starts after creation and ends when it is finally confirmed or conflicts with a confirmed transaction. During the lifecycle, the transaction is in one of the following states.

* Pending
* Confirming
* Confirmed
* Conflicting
* Conflictive
* Reverted
* Abandon

The list does not include orphan transactions that depend on unknown cells, because transactions generator can ignore them.

Different states require different strategies as described in the following chapters.

![transaction-state-diagram](https://raw.githubusercontent.com/r763/uPic/master/202008/IERrxl/transaction-state-diagram.png)

### Pending Transaction

The newly created transaction is in the Pending state.

The generator must store the Pending transactions locally and send them to CKB nodes at regular intervals. It's essential because CKB nodes may drop the transactions in their pools. The generator is not recommended to use the output cells of the pending transactions unless the transaction is stuck and requires fee bumping. If the generator does need chaining pending transactions, it must limit the length of the pending transactions chain.

Once the transaction appears in a block in the canonical chain, it turns to Confirming.

If the Pending transaction or any or its ancestor transaction[^1] has conflict input cells with a transaction in the canonical chain, it becomes conflicting.

If a user or an app decides to give up a stuck transaction, they can mark the Pending transaction is Abandon.

### Confirming Transaction

The Confirming transactions are found in the chain but are not qualified as Confirmed yet.

The generator must store the Confirming transactions locally but does not need to send them to CKB regularly. Same as Pending transactions, it is not recommended to use the output cells of Confirming transactions.

The block containing the transaction gives one confirmation. Each descendant block in the chain gives an extra confirmation. Although any block can be reverted in theory, it is safe to assume that the transaction will never be reverted after X confirmations, where X depends on various factors. The generator has to decide the value of X and adjust it regularly.

The Confirming transaction becomes Confirmed when it gets at least X confirmations.

If a chain reorganization occurs and the block containing the transaction is reverted, the transaction transforms into Pending.

### Confirmed Transaction

A Confirmed transaction is in the chain and has at least X confirmations.

The generator can remove Confirmed transactions from local storage or keep the latest ones as a history for reference. The generator can use the output cells of Confirmed transactions freely.

If a chain reorganization occurs and the block containing the transaction is reverted, the transaction becomes Reverted.

### Conflicting Transaction

A transaction is in the state Conflicting if it conflicts with any transaction in the chain. Two different transactions conflict when

1. They have conflict input cells.
2. A transaction has conflict input cells with any ancestor of another transaction.
3. They are descendants of a pair of conflict transactions.

The generator must store them in the local storage because there is a chance they may become Pending. The generator should not use the output cells of Conflicting transactions.

If all the blocks containing the conflict transactions have been reverted, the Conflicting transactions become Pending again.

If any conflict transaction gets X confirmations, the Conflicting transactions turn to Conflicted. See State "Confirming" for the discussion of X.

### Conflictive Transaction

A Conflictive Transaction conflict with an on-chain transaction that gets at least X confirmations. See State "Confirming" for the discussion of X.

The generator can remove Conflictive transactions from the local storage or keep recent ones for reference. The generator should not use the output cells of Conflictive transactions.

If all the blocks containing the conflict transactions have been reverted, the Conflicted transactions become Pending again.

### Reverted Transaction

State Reverted is an alias of Pending, it is a prompt that the transaction has ever been Confirmed, but is reverted.

The generator must store and send Reverted transactions regularly. The state transformations are the same as Pending.

### Abandon

The generator should allow users to mark a Pending or Reverted transaction as Abandon. The generator stops sending the Abandon transactions to CKB nodes. Nothing can stop a block containing an abandoned transaction. It just means the user has given up the efforts to commit the 
transaction.

The generator must store enough time range of recent Abandon transactions. The generator can clean the old Abandon transactions only when the disk storage is a concern. The reason is mentioned in the RBF fee bumping method below.

User is allowed to mark an Abandon transaction to Pending.

Abandon transactions transform to Confirming or Conflicting just like Pending and Reverted transactions do.

## Fee Bumping

When a transaction is stuck in the Pending or Reverted state for a long time, the generator has two choices.

* CPFP, Child Pays For Parent. The generator creates a child transaction spending the outputs of the stuck transaction.
* RBF, Replace By Fee. The generator marks the stuck transaction as Abandon and uses all or some of its inputs to create a new transaction.

### Fee Estimate For New Transaction

In CKB, the block limits the supply of transaction space in two dimensions:

* The serialized block size including all the transactions.
* The total consumed cycles of all the transactions.

Miners prioritize transaction with higher fee rate $R_t = F_t / b_t$, where $F_t$ is the transaction fee, and $b_t$ is the virtual bytes of a transaction.

\\[
b_t = \max(\frac{c_t L_s}{L_c}, s_t),
\\]

Where

* $L_s$ is the block serialized size limit.
* $L_c$ is the block consumed cycles limit.
* $s_t$ is the serialized size of a transaction $t$ in the block[^2], and
* $c_t$ is its consumed cycles.

Every CKB node has a minimal pool fee rate $\textit{min_fee_rate}_{\textit{pool}}$ which default is 1 Shannons per byte, however, it uses the serialized size instead of virtual bytes. The minimal fee rate determines the minimal fee of a transaction to pay. The generator must call RPC `tx_pool_config`[^3] to get the pool `min_fee_rate` in the unit Shannons per 1000 bytes, and ensure

\\[
F_t \ge \frac{s_t \times \textit{min_fee_rate}_{\textit{pool}}}{1000}
\\]

During transaction congestion in the network, the transactions with the minimal fee will be delayed or even never confirmed. The transaction generator must set a proper fee rate using an estimating algorithm[^4]. Assume that the estimate fee rate is $R_E$, the generator has to set the fee $F_t$ to

\\[
F_t = R_E * b_t
\\]

Because $b_t$ depends on consumed cycles, the generator must figure out the value. There are at last three strategies:

* Run CKB-VM and get the precise consumed cycles.
* Estimate the consumed cycles based on the transaction structure and the scripts to run.
* Use RPC `dry_run_transaction`[^5] to get the serialized size in the block, precise consumed cycles, and virtual bytes.

### CPFP, Child Pays For Parent

CPFP works because the transactions pool in the CKB node prioritizes transactions using ancestor weight.

A transaction A is a parent of another transaction B if at least one of B's input cells is A's output cell. B is called a child transaction of A.

An ancestor of a transaction is either its parent transaction or an ancestor of any its parent.

The ancestor package $A[t]$ of a transaction $t$ is a set that includes itself and all its ancestors remaining in the pool. The weight of the ancestor package $W_{A[t]}$ is the lesser of the transaction fee rate and the package fee rate as defined in the following formula.

\\[
W_{A[t]} = \min(\frac{F_t}{b_t}, \frac{\sum_{i \in A[t]}F_i}{\sum_{i \in A[t]}b_i})
\\]

Recall that $b_t$ is the virtual bytes of a transaction.

The CPFP transaction must have a higher ancestor weight. The generator can follow the recommended instructions below.

1. Estimate a proper fee rate $R_E$ using a fee estimate algorithm.
2. For each parent of the CPFP transaction, call RPC `get_tx_pool_entry`[^6]. The RPC returns the pool entry information when the transaction is in the memory pool. The `tx_pool_config` tells various limits of the pool. The generator must disable CPFP if it will cause its parents to break these limits.

	* The `get_tx_pool_entry.descendant_count` is less than `tx_pool_config.max_descendant_count`.
	* The `get_tx_pool_entry.descendant_vbytes` plus CPFP transaction virtual bytes $b_t$ is less than or equal to `tx_pool_config.max_descendant_vbytes`.

	However, if the CPFP transaction meets the carve-out condition,
	
	* The transaction has only one parent still in the pool, and that parent `get_tx_pool_entry.ancestor_count` is 1.
	* The transaction virtual bytes is at most `tx_pool_config.max_carve_out_vbytes`

	Then the parent descendent package is allowed a bit larger

	* The `get_tx_pool_entry.descendant_count` is less than or equal to `tx_pool_config.max_descendant_count`.
	* The `get_tx_pool_entry.descendant_vbytes` plus CPFP transaction virtual bytes $b_t$ is less than or equal to `tx_pool_config.max_descendant_vbytes + tx_pool_config.max_carve_out_vbytes`.


3. Set a fee so the CPFP ancestor weight is larger than or equal to $R_E$. Let $F_p$ be the sum of `get_tx_pool_entry.ancestor_fee` of all the parents in the pool, and $b_p$ be the sum of `get_tx_pool_entry.ancestor_vbytes`. The CPFP transaction fee $F_t$ is set as

\\[
F_t = R_E * (b_t + b_p) - F_p
\\]

### RBF, Replace By Fee

RBF abandons old transactions and reuse their inputs in new transactions. The RBF transaction must pay enough fee to cover itself and all its replaced transactions.

There are two kinds of RBF transactions, intentional RBF and accident RBF.

If a transaction is stuck and the generator wants to recreate it with a higher fee, it must mark the stuck transaction as Abandon and create a new transaction using the stuck one as the template. The new transaction should keep the inputs and may add new inputs to increase the fee.

If a transaction is stuck and the generator gives up, it must mark the stuck transaction as Abandon. Any new transaction that uses an input which is also used by an Abandon transaction is considered as an RBF transaction.

The RBF transaction fee must ensure its ancestor weight is larger than or equal to the estimated fee rate. The procedure is the same with CPFP transaction using RPC `get_tx_pool_entry` and `tx_pool_config`.

Two transactions conflict if they use the same input, or any of their ancestors are using the same input, or a transaction is using the same input with another's ancestor.

The generator must ensure the fee is large enough that:

* The RBF transaction fee rate is larger or equal to any of the conflict transactions.
* The RBF transaction fee is larger than the total fee of all its conflict transactions. The difference must be larger than or equal to the transaction virtual bytes $b_t$ multiplying `tx_pool_config.min_incremental_fee_rate / 1000`.

[^1]: If a transaction A is a parent of B if B uses an output cell of A as its input cell. An ancestor is either the parent or an ancestor of any parent.
[^2]: In CKB, it is the transaction molecule serialized size plus 4 bytes overhead.
[^3]: The RPC `tx_pool_config` is not ready yet.
[^4]: CKB used to have `estimate_fee_rate` RPC which is deprecated now. A new RPC `get_median_fee_rate` will be added soon and other estimate models will be delivered as a standalone process.
[^5]: The RPC `dry_run_transaction` is not ready yet.
[^6]: The RPC `get_tx_pool_entry` is not ready yet.