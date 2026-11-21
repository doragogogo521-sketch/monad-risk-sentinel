# GitHub 协作交接

## 首次上传

1. 队长创建 `monad-risk-sentinel` 仓库，并邀请另外两位同学。
2. 解压ZIP。将其中 `monad-risk-sentinel` 文件夹内的内容作为仓库根目录，避免再多嵌套一层。
3. 用GitHub Desktop克隆队长仓库，把本文件包中的内容复制进去，检查变更后提交并推送。若已有同名文件，先比较合并，勿直接覆盖队友工作。
4. 网页上传也要先解压并上传目录内容；不要只把ZIP上传为仓库唯一文件。确保根目录显示README.md、frontend、contracts、agent、docs和tests。

本包未创建GitHub仓库、未邀请成员、未推送代码，也不带原托管平台的Git远端。

## 日常协作

- `main`保留能演示的版本。
- 前端分支用`codex/frontend`，合约用`codex/contracts`，Agent用`codex/agent`；团队已有命名规范时沿用团队规范。
- 开工前同步最新main。完成小块功能后发Pull Request，由另一位同学检查再合并。
- frontend主要由前端同学改，contracts由合约同学改，agent由数据同学改。
- 改枚举、单位、哈希算法、ABI或报告结构时，先更新docs/联调基准-v1.md并通知另两位；不应只改单个模块。
- 通过仓库Issue记录阻塞，例如“等待Registry ABI”“确认代币decimals”。

## 首轮联调的完成标准

- 合约同学交付ABI、测试网地址、角色与操作签名。
- Agent同学交付固定回放、符合约定的报告以及获取方式。
- 前端接钱包与合约读取，在真实回执后显示成功；不能只切换本地状态。
- 联合演示一次Registry更新、LTV变化、新借款被拒、还款成功和安全提取；保留可核验交易记录。

## 检查

需要Node.js22或更新版本，从仓库根目录运行 `node --test tests/policy.test.cjs tests/frontend-flow.test.cjs`。启动页面无需Node或npm依赖。

## 发布前

确认README中的模拟/已接入状态与实际一致。仓库是否公开由团队决定；公开发布之前不要把凭证、.env、私钥或助记词放进Git历史。当前.gitignore已包含常见忽略项，但不能移除已提交的秘密。
