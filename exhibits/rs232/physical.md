# 物理边界：先有对象，再谈映射

[展品总览](README.md) · [电气边界](electrical.md) · [来源账本](sources.md)

状态：`stub`。本页只建立已有来源支持的对象边界，**不发布 connector contact 或 pin-to-pin 接线表**。

## 四个文献视角

| 来源 | 本期亲读到的内容 | 不能拿来代替什么 |
|---|---|---|
| V.24 (02/2000)，§1.3 | mechanical characteristics 转引 ISO/IEC 的 25/26/50/37-pole 文献 | 这些 ISO/IEC 文献的实际全文或 contact assignments |
| IBM PC/5150，April 1984，p. 8-4 | 一个 DTE—external modem 图及 25-contact connector 语境 | IBM AT 9-contact 原厂实现，或所有历史机器 |
| IBM AT Serial/Parallel Adapter，所引章页日期 August 31, 1984，pp. 1–2、19–20、24 | 同一卡的 9-contact 串行口与 25-contact 并行口；可选串行线缆另有 25-contact 端；控制器、EIA 收发器与连接器分层 | 任意 PC/AT 或转接线的通用映射、完整标准合规或实际接线安全 |
| TI SLLA037A (September 2002)，pp. 1、7 | 应用笔记讨论 PC 9-contact 接口，使用原词 “DB9S”，并说明该 PC 接口是 full 232 的 subset | 完整 TIA 标准、机械命名裁决或某设备的接线依据 |

来源：[SRC-001](sources.md#src-001)、[SRC-002](sources.md#src-002)、[SRC-004](sources.md#src-004)、[SRC-003](sources.md#src-003)。表中是不同对象/年代的并置，不是发明/普及时间线，也不是证明它们彼此可以直接连接。IBM AT 章节所在卷的版本页为 April 1984，不能用它替换所引章页的 August 31, 1984 日期；书目与文件页映射见 SRC-004。

<a id="ibm-at-three-connectors"></a>

## 同一份手册里的两个“25 接点”，是同一个功能吗？

不是。先区分**卡上的端口**和**可选线缆的一端**，再看原厂给它们的功能名称。IBM AT Serial/Parallel Adapter 这一章让我们在同一个实现语境中比较三个对象：

| 文献中的对象 | 原文接点数 / 形状用词 | 功能语境与定位 |
|---|---|---|
| 卡后部的串行口 | 9-pin D-shell | Serial Portion 下的 RS-232C port；p. 1，串行接口图 p. 19 |
| 可选 IBM Communications Cable (9-Pin) 的另一端 | 25-pin D-shell；与该线缆的 9-pin 端相对 | p. 1 在串行口说明中介绍的通信线缆端，不是卡上的并行口 |
| 卡后部的并行口 | 25-pin D-shell | Parallel Portion：接收八位并行数据的设备语境，原文称 standard TTL levels；p. 20，Parallel Interface 图 p. 24 |

以上均据 [SRC-004，pp. 1、19–20、24](sources.md#src-004)，对应 [CLM-008 / CLM-009](sources.md)。原文中的 TTL 是这个并行功能的电气层描述，**不是把它与 RS-232 线端直连的依据**；本页没有据此整理电压或配线表。

这三个对象说明：**接点数量和 D-shell 外形不足以认出接口功能。** 图中“串行”“并行”和“可选线缆”的对象边界，比只搜“25-pin”多提供了一层信息。此处不判定实物能否机械互插，不推断任意 9-to-25 转接器等同 IBM 的选件，也不从这些章页推出九接点的首次采用年代或设计动机。

<a id="ibm-at-layers"></a>

## 九接点之前，还有控制器与线路接口

回到同章 p. 2 的 **Serial Portion Block Diagram**：IBM 把 asynchronous communications controller、EIA receivers / drivers 和 9-pin connector 分开画出。pp. 1–3 的正文把 framing 放在串行控制器的语境中；TI p. 1 另明确说明 ACE 的并串转换职责。这里的“并串转换”不等于卡上的外部 parallel port。[SRC-004，pp. 1–3](sources.md#src-004)；[SRC-003，p. 1](sources.md#src-003)；[CLM-010](sources.md)。

这样就能把本页接回既有阅读路线：[主机页](host-integration.md)讲的是另一份 IBM PC/5150 文献中的 BIOS/8250 请求；[电气页](electrical.md)区分主机逻辑与 line interface；本章框图则提供一个明确的 IBM AT 适配器实现窗口。三者可以帮助辨认层次，**不能把 PC/5150 的 8250 型号或软件路径移植成这张 AT 卡的已核实事实**。

与 TI 对读时，先比较功能，而不抄接点号：IBM p. 19 从适配器视角区分三条向外、五条向内的数据/控制信号，另列 Signal Ground；TI pp. 1、9 也说明 three transmit / five receive。这里的“三条发出”包括控制功能，不是三条用户数据通道，ground 也不计入三/五。[SRC-004，p. 19](sources.md#src-004)；[SRC-003，pp. 1、7–9](sources.md#src-003)；[CLM-011](sources.md)。

这份对读仍有未解处：IBM p. 1 对指定可选线缆的 25-pin 端使用 “all the signals” 措辞，TI 则称其 PC 接口为 full 232 的 subset。没有相关版本完整标准与该线缆完整资料，不能宣布二者已经完全消歧。TI Figure 6 的 **RST** 原印字样与邻接正文的 **RTS**、IBM p. 20 未知手写标注的处理，均保留在[来源账本的冲突表](sources.md)。

## DE-9、DB-9、DB9 与 DB9S 怎么检索

既有[资料地图](../../research/rs232-source-map.md)保留了这些检索词和来源措辞，采用 DE-9 作为正文命名约定。在这一命名问题上，本页引用亲读的 TI 原词 **DB9S**；没有重新审查地图中的厂商机械命名资料，也不据别名关系推导 serial pin assignment。

同理，`RS-232`、`COM1`、`TTL UART` 不能因为都出现在“串口”检索结果中就成为这个连接器的同义词：主机对象见[BIOS 页](host-integration.md)，电气对象见[电气页](electrical.md)。

## 仍需补齐的证据

2026-09-09 已取得并审阅上述 IBM 9-contact 原厂实现资料，用来限定对读 TI；[资料地图的 Gate 1](../../research/rs232-source-map.md)仅关闭这一来源子项。TIA 官方入口与合法全文、ISO 2110 相关版次全文、版本差异及上述 all-signals/subset 的规范语义仍待核验。不能用 1989/1991 的标准条目倒推 1984 年的机械细节，因此本页保持 `stub`。

本期也没有核实具体两端设备、线缆、接地、供电与热插拔条件。即使认出了连接器，仍须满足[硬件安全检查](../../docs/HARDWARE-SAFETY.md)；当前实验状态为 `blocked-for-hardware`。

[下一站：来源账本](sources.md) · [返回展品总览](README.md)
