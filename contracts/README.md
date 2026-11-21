# 合约同学：接入任务

本目录是合约交接入口，目前没有 Solidity 实现，也没有部署地址。

请先阅读 [联调基准 v1](../docs/联调基准-v1.md)，确认风险枚举与动作编码、LTV策略、TTL和哈希算法；文档编码是提案，不能假定与你的ABI相同。

## 最小交付

1. MonadRiskRegistry：角色控制、riskLevel、两类分数、reasonCode、updatedAt、validUntil、evidenceHash、attestor；支持读取风险状态、查询动作权限和授权提交断言。
2. Reference Lending Pool：GREEN75%、YELLOW60%、ORANGE45%与借款拦截；还款可用；提取需检查抵押约束；RED/UNKNOWN限制见联调基准。
3. 测试网部署：Registry、Pool、mUSD、dUSD四个地址，以及chain ID、RPC、区块浏览器和各代币decimals。
4. 每个合约的ABI JSON，建议放入 `frontend/abi/`；提供借款、还款、抵押、提取与授权的实际函数签名和交易顺序。
5. 一套可重复的部署、测试与回放运行说明。

## 前端等待的答案

- Pool读取Registry动态决定LTV，还是需要单独执行策略应用交易？
- 无记录、过期、未来时间戳、来源不合格时如何处理？
- isActionAllowed只判风险策略，还是也包含用户仓位校验？
- 降LTV后已有债务超出额度时的行为是什么？本原型不会自动清算。
- hash使用SHA-256还是keccak256，哈希的确切字节内容是什么？
- 哪个角色能提交ORANGE/RED，权限、阈值与变更幅度如何校验？

请通过合并申请提交源码与公开部署信息，不要上传私钥或助记词。前端不得接收发布者私钥。
