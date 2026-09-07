# 电气边界：UART 之外还有线路接口

[展品总览](README.md) · 上一站：[IBM 主机路径](host-integration.md) · 下一站：[物理边界](physical.md)

状态：`stub`。本页解释本期材料中的分层，不汇编完整电压/电流/时序规范，不提供连线步骤。

## 两份资料提供的不同证据

IBM 1984 手册 p. 3-3 说明其异步通信适配器的 EIA drivers/receivers 由 **+12 Vdc 和 −12 Vdc** 电源供给，而系统逻辑使用 +5 Vdc。这是该 IBM 电源/适配器语境的描述；**供电轨数值不是线路上每个信号的实测电压，也不是所有 RS-232 设备的统一供电要求**。[SRC-002，p. 3-3](sources.md#src-002)。

TI 的 2002 年应用笔记则在 PC 接口之前区分 UART/ACE：并串转换、start/stop bits 与 parity 生成/检查属于 ACE 的工作。结合 IBM 的 driver/receiver 描述，可以把主机的数据处理与线路接口分开阅读，而不是把 UART 的逻辑侧直接当成外部线端。[SRC-003，p. 1](sources.md#src-003)；[SRC-002，pp. 3-3、5-51–5-53](sources.md#src-002)。

## 规范、实现与实测各回答不同问题

| 类别 | 本期到达哪里 |
|---|---|
| 规范入口 | V.24 §1.2 指向 V.10/V.11/V.12/V.28/V.31/V.31 bis 等 electrical Recommendations；V.24 本身不是这些文献的合并全文 |
| 实现例子 | IBM 文献的供电与 BIOS/8250 分层；不能泛化为所有实现 |
| 实测或仿真 | 均未进行；没有从波形、设备或模拟器得到的新结论 |

规范入口依据：[SRC-001，p. 2](sources.md#src-001)。既有资料地图曾研究 V.28 等其他文献，但这些不计入本期重新审阅并实际引用的 E1 数量；本页不据未重读的条款给出 receiver thresholds 或 polarity 数值。

## 安全停止线

没有选定两端设备与 adapter，也没有完成具体 levels、direction、ground reference、power 和 hot-plug 条件的交叉核验。因此硬件保持 `blocked-for-hardware`。不要因两侧都有 TX/RX/GND 标签就直连 TTL/CMOS UART 与 RS-232 线端，也不要把上述 IBM 供电数字当作试接依据。[硬件安全规则](../../docs/HARDWARE-SAFETY.md)。

完整 TIA/ISO 审阅与设备安全信息仍按[原有资料门禁](../../research/rs232-source-map.md)补齐；[实验页](experiment.md)没有可执行的硬件过程。

[下一站：物理边界](physical.md) · [返回展品总览](README.md)
