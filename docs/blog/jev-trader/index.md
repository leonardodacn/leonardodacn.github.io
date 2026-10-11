# jev-trader 简介


**jev-trader** 是由 Monad 基金会首席AI工程师 Jarrod Watts 开源的AI做市/高频交易机器人，基于 TypeSafe AI 推出的**Jev（TypeSafe System One）快速决策模型**开发，是Jev模型出圈的首个标杆Demo项目。


## 基础信息
- GitHub：`jarrodwatts/jev-trader`，Bun + TypeScript 开发
- 交易标的：Monad 链上 Kuru 交易所 **MON/USDC**
- 演示页面：jev-trader.vercel.app，提供可视化实时仪表盘，展示盘口、模型置信度、成交记录

## 核心机制
1. **决策层：Jev模型**
Jev 不是大语言模型，主打**低延迟实时决策**，目标适配Monad约300ms的出块间隔；读取订单簿数据后输出：买/卖/持有 + 置信概率，只给出交易判断，不生成文本。
2. **执行层：做市限价单**
程序拿到Jev的判断后，在盘口价差内侧挂**仅成交限价单（post-only）**，赚取买卖价差，属于简单链上做市策略。
3. **两种运行模式**
    - Dry-run（默认空跑）：只看盘、做模拟决策，不真实下单，适合调试观察
    - 实盘模式：导入私钥后才会发链上交易

## 项目定位（重点）
作者明确强调：**这只是技术演示Demo，不是稳赚交易策略**，目的是证明Jev模型可以跟上Monad的高速出块节奏，适合AI决策+链上交易的学习、二次开发，不适合直接拿来盈利。

## 社区情况与风险
- 开源后衍生出很多分支版本：比如移植到Hyperliquid的jev-trade，支持BTC/ETH/SOL等合约多空
- 社区有实盘测试案例，出现过短时间大额亏损；AI高置信度≠盈利，缺少成熟回测、风控，市场波动下容易反复频繁换向、持续亏损

## 简单区分
- **Jev**：TypeSafe AI的快速决策模型（System One）
- **jev-trader**：用Jev模型写的Monad链上做市机器人Demo

