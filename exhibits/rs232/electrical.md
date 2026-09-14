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

规范入口依据：[SRC-001，p. 2](sources.md#src-001)。2026-09-14 重读 V.28 (03/1993) 的既有缓存，下面只增加其 significant levels 阅读练习；这不等于完整电气规范或实际接收器验证。[SRC-005，§§2–7](sources.md#src-005)。

<a id="v28-reading"></a>

## 极性侦探：同一个电压，为什么不是同一种答案？

先看电路类别，再看电压。V.28 的 **V1 是 interchange point 相对于 signal ground 或 common return 的电压**，不是电源轨，也不能随意换成对机壳的读数。[SRC-005，§2、Figure 1，p. 1](sources.md#src-005)。

以下数字全是**假设题设**，不是采样、仿真或待执行的测量。采用 V.28 Table 1 的通常极性约定；先按表判断，故障解释与电报特例见题后。展开查看答案；不支持折叠的阅读器可直接顺序阅读。

<details>
<summary>1．四张卡：data / control 各遇到 −6 V、+6 V，分别怎么读？</summary>

| 假设 V1 | Data interchange circuit | Control interchange circuit |
|---|---|---|
| −6 V | binary 1 | OFF |
| +6 V | binary 0 | ON |

Table 1 的两列是 `V1 < −3 V` 与 `V1 > +3 V`。**ON 不是把同一正电压的数据位改叫 1**：数据与控制使用不同的状态名称；§5 对 timing circuit 也使用 ON/OFF。电压符号本身没有一个通用的“逻辑 1”含义。[SRC-005，§5，p. 3；Table 1，p. 4](sources.md#src-005)。

</details>

<details>
<summary>2．V1 = +2 V：数据一定是 0，控制一定是 OFF 吗？</summary>

都不能由 Table 1 得出。+2 V 位于 §5 所说的 transition region（−3 V 与 +3 V 之间），不在表的两个稳定状态列中。这里的答案是**这张表不足以判定**，不是“所有实际接收器输出都必然未定义”；§7 另有依应用而定的故障解释。[SRC-005，§5，p. 3；§7，p. 5](sources.md#src-005)。

</details>

<details>
<summary>3．恰好 +3 V 或 −3 V，能把大于、小于改成包含等号吗？</summary>

不能。+3 V 不满足 `V1 > +3 V`，−3 V 不满足 `V1 < −3 V`；**恰好这两个边界值不属于 Table 1 的任一稳定状态列**。正文使用 “more positive” / “more negative”，表中也是严格不等号；不能改成 `≥` / `≤`，也不能据此预测某个接收器实际输出什么。[SRC-005，§5，p. 3；Table 1，p. 4](sources.md#src-005)。

</details>

<details>
<summary>4．只知道“对机壳 +6 V”，或者“设备有 +12 V 电源”，能查表吗？</summary>

信息不够。前者没有说明机壳与 signal ground/common return 的关系，不能确认题目给的是 V1；后者给的是供电信息，并非 interchange point 的电压。回看本页的 IBM 例子：供电轨不能代替线端状态。[SRC-005，§2、Figure 1，p. 1](sources.md#src-005)；[SRC-002，p. 3-3](sources.md#src-002)。

</details>

### 两条不能省略的限定

**故障解释不是电压查表的隐藏默认值。** §5 明确指向 §7 的例外。§7 说 receiver/load 的故障解释依应用而定：Type 0 不作解释、没有检测能力；Type 1 使 data circuit 采用 binary 1，control/timing 采用 OFF。只有题设另行明确相应故障及 Type 1 解释时，才可按这一项回答；不能看到 +2 V 就自动套用 Type 1，也不能把 Type 0 写成某个固定输出。[SRC-005，§7，p. 5](sources.md#src-005)。

**这不是无例外的家族通则。** §5 的 note 提到：在某些国家、仅直接连接 d.c. telegraph-type circuits 的情况下，Table 1 极性可以反向。本练习不涵盖该特例。§§3–4 的负载/发生器条件与 §6 的动态信号要求也没有被一张静态表代替；能读出假设状态，不等于设备合规、线缆安全或软件已收到字节。[SRC-005，§§3–7，pp. 2–5](sources.md#src-005)。

## 安全停止线

没有选定两端设备与 adapter，也没有完成具体 levels、direction、ground reference、power 和 hot-plug 条件的交叉核验。因此硬件保持 `blocked-for-hardware`。不要因两侧都有 TX/RX/GND 标签就直连 TTL/CMOS UART 与 RS-232 线端，也不要把上述 IBM 供电数字当作试接依据。[硬件安全规则](../../docs/HARDWARE-SAFETY.md)。

完整 TIA/ISO 审阅与设备安全信息仍按[原有资料门禁](../../research/rs232-source-map.md)补齐；[实验页](experiment.md)没有可执行的硬件过程。

[下一站：物理边界](physical.md) · [返回展品总览](README.md)
