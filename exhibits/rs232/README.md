# RS-232：从 DTE/DCE 到 IBM PC 串口

> EIA/TIA-232 family and the PC serial-port implementation：把接口家族、通信角色与具体 IBM 实现分开阅读。

[博物馆首页](../../README.md) · [资料地图](../../research/rs232-source-map.md) · [来源与结论账本](sources.md)

## 身份与本期范围

- Exhibit ID：`rs232`。
- 对象：接口家族及其电气标准语境、主机接口、通信生态；不是某一种插头。
- 状态：`researching`。这是 Gate 2 阅读展品，不是完整 M1 展品。
- 本期切片：保留 2026-09-08 的 V.24 **02/2000** 功能定义、IBM PC/5150 **April 1984** BIOS/8250 个案和 TI **September 2002** 解释；2026-09-09 增补 IBM AT Serial/Parallel Adapter 的连接器/功能对读，所引章页日期为 **August 31, 1984**。
- 生命周期：接口家族的引入、主流期与衰退时间线尚未完成核验；IBM 卷/章日期是文献定位，不是 RS-232 的诞生或九接点首次采用日期。

IBM 手册用外置 modem 说明 DTE 如何接入通信线路；TI 的 2002 年应用笔记则讨论 PC 串口及外围设备。它们提供了不同年代的观察窗口，不能合并成一份没有版本的“串口标准”。[SRC-002，pp. 8-3–8-5](sources.md#src-002)；[SRC-003，p. 1](sources.md#src-003)。

新增的 AT 适配器原厂章节提供一个更具体的问题：一张卡上有九接点串口和二十五接点并口，串口的可选线缆也有二十五接点端；为什么仅认接点数还不够？见[物理页的三个对象对照](physical.md#ibm-at-three-connectors)。[SRC-004，pp. 1、19–20、24](sources.md#src-004)。

## 一条阅读路线

1. [角色与控制信号](protocol.md)：先站在 DTE/DCE 边界上辨认“谁发给谁”，不找针脚号。
2. [IBM 主机路径](host-integration.md)：跟随一次文献中的发送请求，区分数据、控制与软件状态。
3. [电气边界](electrical.md) → [物理边界](physical.md)：用 IBM AT 卡上的端口与可选线缆区分形状/功能，再沿[原厂框图](physical.md#ibm-at-layers)辨认控制器、EIA 收发器与连接器；这仍不足以决定能否接线。
4. [来源账本](sources.md)：按源文献、页码和范围复核；[实验状态](experiment.md)与[后继关系](descendants.md)说明尚未完成什么。

## 两个带答案的观察问题

### “Transmitted data”到了 modem 一侧，还是 modem 的发送输出吗？

不是按设备各自口语中的“发送端”重新命名。V.24 的 circuit 103 是 **To DCE**，104 是 **From DCE**：在这组 DTE/DCE 定义中，103 的数据由 DTE 交给 DCE，104 的数据由 DCE 交给 DTE。先说明角色与观察视角，才能解释 TX/RX；这还不是接线表。[SRC-001，§§3.5–3.6，pp. 4–5](sources.md#src-001)。

继续看[角色表](protocol.md)，再到 IBM 手册 p. 8-4 对照其 **BA/103、BB/104** 的同期标注。对照的是功能名称，不是让 2000 年版本倒过来定义 1984 年硬件。[SRC-002，p. 8-4](sources.md#src-002)。

### BIOS 能返回串口状态，这能告诉我插头是什么吗？

不能由这个软件接口推出连接器身份。IBM 的 `INT 14h` 状态请求把 line status 放在 `AH`、modem status 放在 `AL`；代码按 `RS232_BASE` 访问 8250 的寄存器。这回答的是**软件怎样看到控制器和通信状态**。机械形式与线路电气另需来源，不藏在 `AH`/`AL` 的命名里。[SRC-002，pp. 5-8、5-51、5-53](sources.md#src-002)。

继续看[一次发送的主机路径](host-integration.md)：同一个请求会先处理 modem 控制与状态，再处理发送数据；不能把这些步骤都压成“往 TX 写一个字节”。

## 六层进度

这里的 `documented` 只覆盖 notes 中的本期范围，不表示整个接口家族已经完成研究。

| 层 | 当前可读内容 | 状态 / 尚缺什么 |
|---|---|---|
| Physical | [IBM PC/5150 个案、AT 原厂九接点实现与两种二十五接点功能](physical.md) | `stub`；已补 AT 来源，完整标准/版次和实际映射交叉核验未完成 |
| Electrical | [软件控制器与 line driver/receiver 的边界](electrical.md) | `stub`；完整标准要求、具体设备安全条件未完成 |
| Signaling | [framing 与独立 control circuits 分开](protocol.md) | `stub`；完整时序、速率与版本比较未完成 |
| Protocol / roles | [DTE/DCE、103/104、modem control](protocol.md) | `documented`；仅 V.24 (2000) 的选定功能定义 |
| Host | [IBM 1984 BIOS/8250 读图路径](host-integration.md) | `documented`；仅所引 IBM 实现，不覆盖现代 OS |
| Ecosystem | 外置 modem 个案及[迁移问题](descendants.md) | `stub`；生命周期、替代原因与继承证据未完成 |

## 十个博物馆问题：本期回答到哪里

| 问题 | 入口或明确的未完成项 |
|---|---|
| 何时出现？ | 家族时间线未核验；不以本期文献日期代答 |
| 为何需要它？ | IBM 外置 modem 连接语境，见上文；不是完整起源史 |
| 物理接口是什么？ | [物理页](physical.md)：实现与标准分开，映射仍受门禁约束 |
| 电气规则是什么？ | [电气页](electrical.md)：本期仅解释边界，非完整规范 |
| 数据、控制、时钟怎样分工？ | [角色页](protocol.md)：数据/control 区分；完整 timing 尚未覆盖 |
| 怎样寻址、选择、仲裁？ | 本期不泛化；V.24 的适用范围并非只限一种网络拓扑 |
| 主机怎样驱动？ | [IBM 个案](host-integration.md)；现代发现/驱动路径未研究 |
| 使用者需要理解什么？ | 角色、配置参数、控制状态分别查证；本期不声称统计了历史故障频率 |
| 为什么退出主流？ | [后继页](descendants.md)：尚缺具体使用场景与年代证据 |
| 什么得以保留？ | 暂不建立无来源的继承/兼容边，见[关系状态](descendants.md) |

V.24 §1.1 列举同步/异步以及多种线路服务情形；本期的外置 modem 阅读路线不是对整个 Recommendation 拓扑的概括。[SRC-001，pp. 1–2](sources.md#src-001)。

## 证据与安全状态

本期实际使用 **3 份 E1、1 份 E2**，见[来源账本](sources.md)；新 IBM 章节按一份原厂文献计数，扫描/OCR/多个页面不重复计数，TI 仍是 E2。E1 并不等于“所有页面都完成验证”。没有运行仿真（E3），没有测量硬件（E4）。硬件状态为 `blocked-for-hardware`。

IBM 9-contact 原厂资料获取/审阅子项已完成；TIA 官方入口/合法全文、ISO 2110 相关版次全文和标准版本对照等[原有门禁](../../research/rs232-source-map.md)仍未关闭。IBM 的 all-signals 与 TI 的 subset 措辞尚未完成规范语义消歧，详见[冲突账本](sources.md)。不得依本文或相似的 TX/RX/GND 名字直接接线，不提供 pin-to-pin、null-modem 制作或热插拔步骤。参见[硬件安全规则](../../docs/HARDWARE-SAFETY.md)。

本展品新增的是**读者可跟随的跨层问题、页间导航和可追溯来源**，不是重新抄写 pinout，也不是把研究状态换个名字标成完成。
