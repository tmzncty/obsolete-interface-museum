# 物理边界：先有对象，再谈映射

[展品总览](README.md) · [电气边界](electrical.md) · [来源账本](sources.md)

状态：`stub`。本页只建立已有来源支持的对象边界，**不发布 connector contact 或 pin-to-pin 接线表**。

## 三个文献视角

| 来源 | 本期亲读到的内容 | 不能拿来代替什么 |
|---|---|---|
| V.24 (02/2000)，§1.3 | mechanical characteristics 转引 ISO/IEC 的 25/26/50/37-pole 文献 | 这些 ISO/IEC 文献的实际全文或 contact assignments |
| IBM April 1984，p. 8-4 | 一个 DTE—external modem 图及 25-contact connector 语境 | 后来的 PC 9-contact 原厂实现，或所有历史机器 |
| TI SLLA037A (September 2002)，pp. 1、7 | 应用笔记讨论 PC 9-contact 接口，使用原词 “DB9S”，并说明该 PC 接口是 full 232 的 subset | 完整 TIA 标准、机械命名裁决或某设备的接线依据 |

来源：[SRC-001](sources.md#src-001)、[SRC-002](sources.md#src-002)、[SRC-003](sources.md#src-003)。表中是不同对象/年代的并置，不是证明它们彼此可以直接连接。

## DE-9、DB-9、DB9 与 DB9S 怎么检索

既有[资料地图](../../research/rs232-source-map.md)保留了这些检索词和来源措辞，采用 DE-9 作为正文命名约定。本期只引用亲读的 TI 原词 **DB9S**；没有重新审查地图中的厂商机械命名资料，也不据别名关系推导 serial pin assignment。

同理，`RS-232`、`COM1`、`TTL UART` 不能因为都出现在“串口”检索结果中就成为这个连接器的同义词：主机对象见[BIOS 页](host-integration.md)，电气对象见[电气页](electrical.md)。

## 仍需补齐的证据

沿用[资料地图的 Gate 1](../../research/rs232-source-map.md)：TIA 官方入口与合法全文、ISO 2110 相关版次全文、IBM 9-contact 原厂资料，以及版本差异的交叉核验尚未完成。不能用 1989/1991 的标准条目倒推 1984 年的机械细节。

本期也没有核实具体两端设备、线缆、接地、供电与热插拔条件。即使认出了连接器，仍须满足[硬件安全检查](../../docs/HARDWARE-SAFETY.md)；当前实验状态为 `blocked-for-hardware`。

[下一站：来源账本](sources.md) · [返回展品总览](README.md)
