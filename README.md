# Monad Risk Sentinel

**From Real-World Events to On-chain Risk Intelligence.**

面向 Monad DeFi 的事件驱动风险情报 MVP。当前交付为可交互的前端模拟原型：固定事件 → 机构关联 → 稳定币敞口 → ORANGE 风险断言 → 示例借贷池 LTV 从 75% 调至 45%，禁止新增借款，保留还款与满足抵押约束的退出。

> 当前没有连接 AI、钱包、Monad RPC 或真实合约；机构、资产、价格、持仓与证据均为模拟。链上地址和交易哈希尚待接入，不是已部署的完整基础设施。

## 先启动页面

需要 Python 3，无需安装第三方依赖。

1. 解压后进入本 README 所在的 `monad-risk-sentinel` 目录。
2. 在终端运行：

```sh
python3 -m http.server 8765 --bind 127.0.0.1 --directory frontend
```

Windows 如果没有 `python3` 命令，改用：

```powershell
py -3 -m http.server 8765 --bind 127.0.0.1 --directory frontend
```

3. 在同一台电脑浏览器打开 http://127.0.0.1:8765/ 。
4. 保持终端运行；停止服务按 Ctrl+C。请不要直接双击 HTML 文件，报告哈希需要 localhost 或 HTTPS 安全上下文。

端口被占用时将命令和浏览器地址中的 `8765` 同时改为 `8766`。

## 演示流程

点击“开始引导演示”，每步由用户点击确认：

1. 有效 GREEN 基线下借入 100 dUSD：债务从 200 变为 300。
2. 查看三份模拟证据：托管限制、稳定币关联、链上状态快照。
3. 回放事件并发布 ORANGE：LTV 从 75% 变为 45%。
4. 验证新增借款被拒绝，债务与钱包余额不变。
5. 还款 50 dUSD：债务变为 250。
6. 提取 100 mUSD：抵押由 1,000 变为 900，仍满足抵押约束。

完成后可推进模拟时间至 TTL 之后：有效状态变为 UNKNOWN，原始断言保留 ORANGE，LTV 保持 45%，不自动恢复借款。刷新或重置会清除本地演示状态。

## 目录与分工

```text
frontend/           页面、样式、交互、共享策略与报告 Schema
contracts/          合约同学的接入任务；尚无合约实现
agent/              Agent 同学的接入任务与模拟报告样例；尚无 Agent 服务
docs/              产品文档、联调基准、启动和 GitHub 协作说明
tests/             策略与前端流程检查
.github/            合并申请模板
```

- [三方联调基准 v1](docs/联调基准-v1.md)：先统一风险等级、策略、单位、哈希和接口。
- [合约同学接入任务](contracts/README.md)。
- [Agent 同学接入任务](agent/README.md)。
- [启动与演示说明](docs/启动与演示.md)。
- [GitHub 协作说明](docs/GitHub协作.md)。
- [原始产品文档](docs/产品文档原件.md)：原样保留；冲突处以团队确认后的联调基准为准。

## 运行检查

可选：安装 Node.js 22 或更新版本后，从仓库根目录运行，无需 npm install：

```sh
node --test tests/policy.test.cjs tests/frontend-flow.test.cjs
```

覆盖风险枚举、TTL、LTV 上限、借款拦截、还款、提取约束、报告生成失败、引导流程与重置。流程测试使用模拟 DOM；不等同于真实浏览器、钱包或链上验收。

## 当前状态与下一步

前端、报告样例、共享策略和协作文件已准备；真实合约、Agent、数据源、钱包与回执尚未接入。风险分数是固定演示参数，不是经过校准的损失预测。

数值编码和 YELLOW=60% 是联调提案，尚未获合约实现确认。接入时以确认后的 ABI、代币精度和真实回执为准。

该目录可以直接作为 GitHub 仓库根目录。文件包不包含原工作区的凭证、Git 历史、私有托管配置或全局技能。
