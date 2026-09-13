# RS-232 阅读展品：来源与结论账本

[展品总览](README.md) · [角色页](protocol.md) · [IBM 主机页](host-integration.md) · [完整研究地图](../../research/rs232-source-map.md)

## 本期审阅范围

初始切片核验日期：**2026-09-08**。通过正常公开入口取得 SRC-001 至 SRC-003，亲读所列章节；IBM PC/5150 扫描的封面与关键 BIOS 清单另经页面图像核对。

**2026-09-09 增补**：取得并审阅 SRC-004 的 IBM AT 适配器章节，核对卷/章身份与关键原图；复用既有 TI PDF 对读其 pp. 1、7–9。新增核验不表示重新审阅了旧切片的每一页。只在仓库记录引用与结论，不提交下载的全文或扫描图。

实际使用的 E1 数由 2 份增至 3 份，目前共 **3 份 E1（V.24、IBM PC/5150 手册、IBM AT 适配器章节）和 1 份 E2（TI 应用笔记）**。新增 IBM 文献的 PDF、OCR、多个页面和多次复核只计一份 E1。研究地图中的其他来源不因被列在那里就自动算作本展品实际使用的 E1；原地图的 2026-09-01 记录与两次切片核验分开保留。

## Source ledger

<a id="src-001"></a>

### SRC-001 — ITU-T V.24

- **Evidence level:** E1。
- **Author / organization:** International Telecommunication Union, ITU-T。
- **Document / version / date:** Recommendation V.24 (02/2000), *List of definitions for interchange circuits between data terminal equipment (DTE) and data circuit-terminating equipment (DCE)*；批准日期 17 February 2000。
- **Location:** [官方文献入口](https://www.itu.int/rec/T-REC-V.24-200002-I/en)；[入口所列英文 PDF](https://www.itu.int/rec/dologin_pub.asp?lang=e&id=T-REC-V.24-200002-I!!PDF-E&type=items)。
- **Pages / section:** 正文 pp. 1–7：§§1.1–1.4、§2、Table 1、§§3.5–3.12；p. 17：§§4.5–4.7。下载 PDF 的文件页 7–13 对应正文 1–7，文件页 23 对应正文 17；标题/批准日期见文件页 1、3。
- **Used for:** DTE/DCE 视角、数据与控制 circuits 的方向/分工、按应用选用 circuits，以及 electrical/mechanical 文献边界。
- **Scope:** 2000 年 V.24 文献的定义与范围；不是 TIA-232 各版本或所有历史 PC 的合规证明。
- **Notes:** §1.2 把电气特性指向其他 Recommendations；§1.3 指向 ISO/IEC 机械文献。下载全文不等于已审阅其中所有条款；本期不据 §4.7 推断设备可以热插拔。
- **Research-map ID:** S2。

<a id="src-002"></a>

### SRC-002 — IBM Personal Computer Technical Reference

- **Evidence level:** E1。
- **Author / organization:** International Business Machines Corporation。
- **Document / version / date:** *Personal Computer Technical Reference*, Revised Edition, April 1984，publication **6361453**。
- **Location:** [Internet Archive 文献入口](https://archive.org/details/IBMPCIBM5150TechnicalReference6322507APR84)；[该条目的 PDF 扫描](https://archive.org/download/IBMPCIBM5150TechnicalReference6322507APR84/IBM%20PC%20IBM_5150_Technical_Reference_6322507_APR84.pdf)。
- **Pages / section:** 封面、修订页、末尾 Reader's Comment Form；正文 pp. 3-3、5-8、5-50–5-53、8-3–8-5。
- **Used for:** IBM PC/5150 的 EIA driver/receiver 供电语境、BIOS 数据区、8250 base address、`INT 14h` 服务与发送/状态清单、DTE—外置 modem 个案及同期 circuit 名称。
- **Scope:** 该 IBM 原厂技术参考描述的实现与历史措辞；不是所有兼容机、现代 OS 或具体 USB adapter 的行为。
- **Notes:** Archive identifier、URL 和 PDF 文件名使用 **6322507**，但扫描封面与 Reader's Comment Form 为 **6361453**；引用保留检索 URL，以文献内编号为准。页码是书内印刷页码，不是 PDF viewer 页序。
- **Research-map ID:** S5。

| 本期引用的印刷页 | 此次 309 页扫描中的文件页 | 复核重点 |
|---|---:|---|
| 封面 / 修订页 / Reader's Comment Form | 1 / 3 / 308 | 6361453 / April 1984 / 6361453 |
| 3-3 | 74 | EIA drivers/receivers 与逻辑供电的不同语境 |
| 5-8 | 101 | BIOS 数据区保存卡的 base addresses |
| 5-50 | 143 | `INT 14h` 服务与参数注释 |
| 5-51 | 144 | line/modem status、8250 base address 与分支选择 |
| 5-52 | 145 | 初始化、发送控制状态等待与字符写入 |
| 5-53 | 146 | 接收尾部、状态读取、`WAIT_FOR_STATUS` |
| 8-3–8-5 | 252–254 | DTE/DCE、外置 modem、25-contact 语境及同期说明 |

OCR 对汇编操作数有误识别，本期对 pp. 5-51–5-52 的关键字段核对了扫描图。后续复核亦应回到原图，不复制 OCR 错字。p. 5-54 已进入键盘 `INT 16h` 清单，不纳入本期串口代码定位。

<a id="src-003"></a>

### SRC-003 — TI Interface Circuits for TIA/EIA-232-F

- **Evidence level:** E2，后续技术应用笔记，不升级为标准全文。
- **Author / organization:** Texas Instruments。
- **Document / version / date:** *Interface Circuits for TIA/EIA-232-F*, **SLLA037A，September 2002**。
- **Location:** [TI 官方 PDF](https://www.ti.com/lit/an/slla037a/slla037a.pdf)。
- **Pages / section:** p. 1，General Information / TIA/EIA-232-F Industry Standard for Data Transmission；p. 7，The DB9S Connector / Figure 6；pp. 8–9 的邻接信号说明与 Figure 8 分层例子。2026-09-09 再次核对这些原图，用于与 SRC-004 的功能/分层对读；不将其中的配线图转成操作建议。此次 PDF 文件页 5、11–13 分别对应印刷页 1、7–9。
- **Used for:** UART/ACE 的 framing 角色、该笔记聚焦 PC 9-contact subset 的范围、不同外围设备的应用语境及原词 DB9S；three transmit / five receive 的功能分组及其与 IBM 指定实现的限定对照。
- **Scope:** TI 2002 年对 PC 接口的后续解释，不代替 E1 标准、原厂机器手册或特定设备验证。
- **Notes:** 其“physical layer”措辞涵盖电气讨论；本仓仍按自己的六层模型分开 electrical 与 mechanical。本期不据其简介填入完整起源/衰退时间线，不采用它作为机械命名裁决或 null-modem 接线依据。
- **Research-map ID:** S8。

<a id="src-004"></a>

### SRC-004 — IBM AT Serial/Parallel Adapter

- **Evidence level:** E1，原厂技术参考中的指定适配器章节。
- **Author / organization:** International Business Machines Corporation。
- **Document / version / date:** *Personal Computer Hardware Reference Library — Technical Reference — Options and Adapters, Volume 2*；卷首为 **Revised Edition (April 1984)**。所用章标题为 *Serial/Parallel Adapter*，标题页边栏指名 **IBM Personal Computer AT Serial/Parallel Adapter**；本次所引正文页脚为 **August 31, 1984**。卷日期与章页日期分开记录，不用文件名的 `Apr84` 替换章页日期，也不据此猜测扫描的装订/增补过程。
- **Publication / part number:** 本次核验页未确认独立编号；不从 SRC-002 或另一本 AT 系统主手册移用编号。以卷名、章名、版本/章页日期、精确页码及下列扫描哈希识别本次引用。
- **Location:** [Internet Archive 文献入口](https://archive.org/details/bitsavers_ibmpccardsptionsandAdaptersVolume2Apr84_25079400)；[本次所用 PDF 扫描](https://archive.org/download/bitsavers_ibmpccardsptionsandAdaptersVolume2Apr84_25079400/Technical_Reference_Options_and_Adapters_Volume_2_Apr84.pdf)。2026-09-09 经正常公开入口取得；仅归档引用，不复制扫描进仓库。
- **Pages / section:** 卷标题/版本、章标题/目录及正文 pp. 1–3、19–20、24，文件页映射见下表。只采用列出的功能说明/原图，不声称完整阅读全卷或审查所有寄存器、规格及原理图。
- **Used for:** 明确的原厂九接点串行实现；卡上的串/并端口与可选串行线缆端的不同对象；controller、EIA receivers/drivers 与 connector 分层；串行图的数据/控制功能与 SRC-003 的限定对读。
- **Scope:** 所引 IBM AT 适配器及文献所述可选 IBM Communications Cable (9-Pin)，不是全部 PC/AT、兼容卡或任意 9-to-25 转接器；不是完整标准合规或实物安全验证。
- **Notes:** PDF 为 692 文件页、25,079,400 bytes；SHA-256 `b5bf24ea3e63082d5c637db8b08469c6d4929b4b9f6b7b24c7a211338b42a15f`。文件大小及 SHA-1 `14175f624c7822071ebc2d2cd2e8edf4b66aeec3` 与 Archive 元数据一致；OCR 仅作定位，关键图和卷/章身份另经视觉复核。获取记录与范围另见研究地图 S13。
- **Research-map ID:** S13。

以下 PDF 页均为从 1 开始的文件页序，不是全卷统一连续的印刷页码。

| 文献位置 / 印刷页 | 此次 692 页扫描中的文件页 | 复核重点 |
|---|---:|---|
| 卷标题 / 版本页 ii | 2 / 3 | Options and Adapters / Volume 2；Revised Edition (April 1984) |
| AT 适配器章标题 / Contents iii | 494 / 496 | 适配器身份；Serial 与 Parallel 是本章不同部分 |
| 1 | 498 | 同一卡两个功能、9-pin 串行口及可选 9/25 通信线缆 |
| 2 | 499 | Serial Portion Block Diagram：controller、EIA receivers/drivers、9-pin connector |
| 3 | 500 | Communications Application 与 framing 的邻接范围；不采用 jumper 操作 |
| 19 | 516 | 串行图的适配器/External Device 观察边界与数据/控制分组 |
| 20 | 517 | Parallel Portion 首段的八位数据、standard TTL levels、25-pin D-shell；不采用未知手写 J2 改标 |
| 24 | 521 | Parallel Interface 图及并行设备语境 |

上述正文所引页脚均为 August 31, 1984。p. 19 / p. 24 的图用于核验对象和功能，不被转抄为接点表、pin-to-pin 表或配线图。p. 20 的手写风险和 p. 1 的 all-signals 措辞保留在下方冲突表。

## Claim ledger

`confirmed` / `supported` 仅指所列文献范围内的证据状态，不代表实测或完成整个展品。

| Claim ID | 可核验结论 | 层 | Source(s) / 定位 | Scope | Confidence |
|---|---|---|---|---|---|
| CLM-001 | V.24 将功能定义与另行引用的 electrical/mechanical 特性分开 | protocol / physical / electrical | SRC-001，§§1.1–1.3，pp. 1–2 | V.24 (2000) 文献结构 | confirmed |
| CLM-002 | 103 To DCE、104 From DCE；选定 control circuits 各有方向与条件 | protocol | SRC-001，Table 1、§§3.5–3.12，pp. 3–7 | V.24 (2000)，非 contact assignment | confirmed |
| CLM-003 | 实际设备按应用选择 circuits；data/control 分类不等于 UART framing | signaling / protocol | SRC-001，§1.1、Table 1、§4.5；SRC-003，p. 1 | 规范功能分类与 TI 对 PC ACE 的解释分别成立 | supported |
| CLM-004 | IBM BIOS 数据区保存卡基址，`INT 14h` 提供初始化/发送/接收/状态服务，状态请求分开返回 line/modem status | host | SRC-002，pp. 5-8、5-50–5-53 | IBM April 1984 所载实现 | confirmed |
| CLM-005 | 该 IBM 发送分支先设 DTR/RTS，等 DSR/CTS，再等发送 holding register 就绪后写字符，等待可超时 | host | SRC-002，p. 5-52 lines 1698–1727；p. 5-53 lines 1763–1789 | 原厂清单分析；不是执行 trace 或通用串口算法 | confirmed |
| CLM-006 | IBM 文献中的 EIA drivers/receivers 供电与主机逻辑/8250 角色应分开读 | electrical / host | SRC-002，pp. 3-3、5-51–5-53；SRC-003，p. 1 | IBM 实现与 TI 的 ACE 分层解释 | supported |
| CLM-007 | IBM 外置 modem/25-contact 个案与 TI 后续 PC 9-contact subset 是两个受限定的观察窗口 | physical / ecosystem | SRC-002，pp. 8-3–8-5；SRC-003，pp. 1、7 | 1984 IBM 与 2002 TI 文献，非普遍映射/替代链 | supported |
| CLM-008 | 指定 IBM AT 适配器同时提供 9-contact 串行口和 25-contact 并行口；后者有八位并行数据及 standard TTL levels 的原文语境 | physical / signaling / electrical | SRC-004，pp. 1、19–20、24 | 仅此适配器文献，不是通用接点/电压要求 | confirmed |
| CLM-009 | 文献所述可选串行通信线缆另有 25-contact 端，与卡的 25-contact 并行口是不同对象；接点数/外形不足以认定功能 | physical / ecosystem | SRC-004，pp. 1、20、24 | 文献内部对象对照，不证明任意线缆映射、实物互插或电气兼容 | confirmed |
| CLM-010 | AT 串行框图将 communications controller、EIA receivers/drivers 与 9-pin connector 分开；并串转换不等于外部 parallel port | physical / electrical / host | SRC-004，pp. 1–3；对读 SRC-003，pp. 1、9 Figure 8 | 各自实现的分层证据，不互相移植芯片型号或软件路径 | confirmed |
| CLM-011 | IBM 串行图从适配器视角的三发五收数据/控制分组，与 TI 的 three transmit / five receive 说明可限定对读；Signal Ground 另列 | signaling / roles | SRC-004，p. 19；SRC-003，pp. 1、7–9 | 功能分组对照；三发不是三条用户数据通道，不解决全部标准 circuits 或接线 | supported |

## 冲突与不采用的推论

| 事项 | 本期处理 |
|---|---|
| IBM p. 8-3 称 V.24 “equivalent to” RS-232C | 保存为 1984 同期表达；不写无版次的 `V.24 = RS-232`。SRC-001 (2000) 自身明确分派功能、电气与机械文献。 |
| IBM `Clear to Send` 与 V.24 `Ready for sending` | 保留各自名称；通过 IBM p. 8-4 的 circuit 106 标注对读，不悄悄改写源文献。 |
| DB9S / DE-9 等名称 | TI 原词不改；地图中的命名研究仍可检索，但本期不冒称重新读过其余厂商来源。 |
| IBM AT 卷 April 1984 / 所引章页 August 31, 1984 | 两层日期分别引用；文件名不替换章页日期，不从文献日期推定九接点首次采用，也不把 TI 的后续缩小空间描述写成 IBM 设计动机。 |
| IBM 可选线缆的 all-signals / TI 的 PC subset | SRC-004 p. 1 在该线缆连接到指定适配器的条件下，称其 25-pin 端 “has all the signals of a standard EIA RS-232C interface”；SRC-003 p. 1 则称所述 PC 接口为 full 232 的 subset。保留各自对象和措辞；没有相关版本完整标准及线缆完整资料，不能宣布完全消歧、已证实全标准合规或 TI 被推翻。 |
| TI Figure 6 原印 RST / 邻接正文 RTS | SRC-003 p. 7 图 6 代码栏原图印 **RST**，描述为 Request To Send；p. 8 标题与 p. 9 Figure 7 使用 **RTS**。记录为来源内部不一致，不静默改字，不说成 OCR 错字。 |
| IBM p. 20 的手写 J2 / Port 改标 | 来源、正确性与对应卡修订未知；只采用未受改标影响的首段功能文字，不采用 J2 设置，也不把手写当作原厂授权勘误。 |
| IBM AT 原图 / 其他来源的芯片或几何细节 | 不从 SRC-002 的 8250 或 SRC-003 的器件例子推断 AT 卡芯片；不猜 connector gender、mating/solder view，也不将 controller pin 编号混成外部 connector contact 编号。 |
| TIA-232-F / ISO 2110 全文与版本 | 本期未取得/审阅；原地图中的第三方 TIA 预览和 ISO catalog 记录不视为全文，也不增加本期 E1 计数。 |
| 现代 USB adapter / tty / COM | 没有本期产品或驱动证据，不推断通用 buffering、signal 暴露或兼容行为。 |
| E3/E4 与本期阅读 | 均未执行；文献清单的导读不作为实验结果。 |

## 完成门槛

IBM 九接点原厂实现的获取/审阅子项已完成，实际增量见[三个连接器对象的导读](physical.md#ibm-at-three-connectors)和[AT 分层框图路线](physical.md#ibm-at-layers)。这不关闭整个 Gate 1：完整电气/机械标准与版本、all-signals/subset 的规范语义、生命周期、关系、设备安全与实验等缺口仍见[总览](README.md)、[实验页](experiment.md)及[原资料地图](../../research/rs232-source-map.md)。展品保持 `researching`、physical `stub` 和 `blocked-for-hardware`，没有 E3/E4；没有关键来源的地方保留未知，不以增加元数据完整度代替研究。
