# RS-232 阅读展品：来源与结论账本

[展品总览](README.md) · [角色页](protocol.md) · [IBM 主机页](host-integration.md) · [完整研究地图](../../research/rs232-source-map.md)

## 本期审阅范围

核验日期：**2026-09-08**。通过正常公开入口取得下列文献，亲读所列章节；IBM 扫描的封面与关键 BIOS 清单另经页面图像核对。只在仓库记录引用与结论，不提交下载的全文或扫描图。

本期共使用 **2 份 E1（V.24、IBM 手册）和 1 份 E2（TI 应用笔记）**。研究地图中的其他来源不因被列在那里就自动算作本展品实际使用的 E1；原地图的 2026-09-01 核验记录与本期记录分开保留。

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
- **Pages / section:** p. 1，General Information / TIA/EIA-232-F Industry Standard for Data Transmission；p. 7，The DB9S Connector。另读 pp. 8–9 的邻接说明以确认范围，不将其中的配线图转成操作建议。此次 PDF 文件页 5、11 分别对应印刷页 1、7。
- **Used for:** UART/ACE 的 framing 角色、该笔记聚焦 PC 9-contact subset 的范围、不同外围设备的应用语境及原词 DB9S。
- **Scope:** TI 2002 年对 PC 接口的后续解释，不代替 E1 标准、原厂机器手册或特定设备验证。
- **Notes:** 其“physical layer”措辞涵盖电气讨论；本仓仍按自己的六层模型分开 electrical 与 mechanical。本期不据其简介填入完整起源/衰退时间线，不采用它作为机械命名裁决或 null-modem 接线依据。
- **Research-map ID:** S8。

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

## 冲突与不采用的推论

| 事项 | 本期处理 |
|---|---|
| IBM p. 8-3 称 V.24 “equivalent to” RS-232C | 保存为 1984 同期表达；不写无版次的 `V.24 = RS-232`。SRC-001 (2000) 自身明确分派功能、电气与机械文献。 |
| IBM `Clear to Send` 与 V.24 `Ready for sending` | 保留各自名称；通过 IBM p. 8-4 的 circuit 106 标注对读，不悄悄改写源文献。 |
| DB9S / DE-9 等名称 | TI 原词不改；地图中的命名研究仍可检索，但本期不冒称重新读过其余厂商来源。 |
| TIA-232-F / ISO 2110 全文与版本 | 本期未取得/审阅；原地图中的第三方 TIA 预览和 ISO catalog 记录不视为全文，也不增加本期 E1 计数。 |
| 现代 USB adapter / tty / COM | 没有本期产品或驱动证据，不推断通用 buffering、signal 暴露或兼容行为。 |
| E3/E4 与本期阅读 | 均未执行；文献清单的导读不作为实验结果。 |

## 完成门槛

虽然本期有 E1 来源，展品仍为 `researching`。完整电气/机械标准、生命周期、关系、设备安全与实验等缺口见[总览](README.md)、[实验页](experiment.md)及[原资料地图](../../research/rs232-source-map.md)。没有关键来源的地方保留未知，不以增加元数据完整度代替研究。
