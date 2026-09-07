# 实验状态：目前是文献导读

[展品总览](README.md) · [主机清单导读](host-integration.md) · [来源账本](sources.md)

## 没有已执行的实验

本期没有启动模拟器、操作串口设备、接线或采样。

- E3：未执行，没有 emulator/version/config 或运行结果。
- E4：未执行，没有设备 setup、波形或观测结果。
- Hardware status：`blocked-for-hardware`。

[主机页](host-integration.md)的发送流程来自 IBM 原厂手册，属于 E1 文献分析，**不是实机 trace 或仿真结果**。普通文档/元数据测试也不构成 E3 硬件仿真证据。

## 未来实验与本期的边界

[原资料地图](../../research/rs232-source-map.md)提出过“指定 USB–serial adapter 的 local loopback 与 line-side sample”，并明确尚未执行。本期不把它改写成可以直接运行的步骤，也没有选定 adapter。

开始硬件工作前仍须补齐地图 Gate 1/Gate 3 和[硬件安全记录模板](../../docs/HARDWARE-SAFETY.md)：两端设备、具体线缆/breakout、供电状态、已核实的电平/方向/地参考/供电关系、测量工具及输入限制、probe point、sample rate、OS/driver/config、日期、安全依据与不确定性。任何安全关键项未知，都不能通过写一份 procedure 来视为解决。

软件 loopback、真实 adapter 线端测量与 legacy DTE↔DCE 互连应保留各自问题和结果范围，不能互相替代；依据是[证据分层](../../docs/EVIDENCE.md)和原资料地图的 Gate 3。

## 当前可复核的事情

现在可以不接触硬件地沿[来源账本](sources.md)打开文献，在 IBM p. 5-52 找到 modem-control、status-wait 和字符输出的不同位置，再与[角色页](protocol.md)对读。这个阅读练习只能复核文献解释，不能验证线端符合规范或远端已收到数据。

[返回展品总览](README.md)
