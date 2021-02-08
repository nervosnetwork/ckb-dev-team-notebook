# Data Hash Syscall Postmortem

## Incident date(s)

2020-07-30 - 2020-08-10

## Authors

@zhangsoledad 

## Summary

syscall `load_cell_by_field` 被设计为可以通过设置参数来获取input data hash. 但目前并不能正常工作，且使用次 syscall 的交易在交易池验证阶段会有不确定性结果，对最终链上确认没有影响，但实质形成一条怪异的规则：对于使用 `load_cell_by_field` 获取 input data hash 的交易，如果其所需要获取的 input 所指向的交易与当前交易在同一区块且序列在前，则 syscall 能执行成功，否则失败。

## Causes

目前代码在 resolve transaction 时，通过参数 with_data 控制是否在内存中加载对应 outpoint 所指向 output 的 data 到内存中。
对于 input ，with_data 设为了 false，https://github.com/nervosnetwork/ckb/blob/805a15ecfad619f4f1e21800507bdba09368d1b0/util/types/src/core/cell.rs#L452-L461

https://github.com/nervosnetwork/ckb/blob/805a15ecfad619f4f1e21800507bdba09368d1b0/script/src/syscalls/load_cell.rs#L100-L107
syscall load_cell 目前实现如果内存中没有加载 data, 返回 `ITEM_MISSING` error
所以 syscall `load_cell_by_field` 用来获取input data hash，目前不能正常运行。

由于部分 CellProvider 的实现错误：
1. https://github.com/nervosnetwork/ckb/blob/805a15ecfad619f4f1e21800507bdba09368d1b0/util/types/src/core/cell.rs#L277-L278
导致链上确认实质形成一条怪异的规则：对于使用 `load_cell_by_field` 获取 input data hash 的交易，如果其所需要获取的 input 所指向的交易与当前交易在同一区块且序列在前，则 syscall 能执行成功，否则失败。

2. https://github.com/nervosnetwork/ckb/blob/805a15ecfad619f4f1e21800507bdba09368d1b0/tx-pool/src/component/pending.rs#L106-L107 https://github.com/nervosnetwork/ckb/blob/805a15ecfad619f4f1e21800507bdba09368d1b0/tx-pool/src/component/proposed.rs#L90-L91
导致交易池验证会有不确定性。

## Resolution

https://github.com/nervosnetwork/ckb/commit/4fdaff86df3bc0bf260efe4c908a9f40e5849dee
修复忽略 with_data 参数的 CellProvider 实现，修复不确定性。
目前仍保持 syscall `load_cell_by_field` 获取 input data hash 不可用，于之后通过 hard fork 来进行修复。

## Detection

2020-07-30 @huwenchao 报告由 @xxuejie  转发

## Lessons Learned

### What went wrong

一些逻辑流程没有被测试覆盖，需要长期不断完善

### Where we got lucky

链上校验虽然出现一条意料之外的规则，但还是确定性的。
