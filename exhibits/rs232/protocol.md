# 角色、数据与控制：先问谁对谁说话

[展品总览](README.md) · 下一站：[IBM 主机路径](host-integration.md) · [来源账本](sources.md)

## 范围

本页主要读 **ITU-T V.24 (02/2000)** 的 interchange circuits 功能定义。V.24 §1.2 把 electrical characteristics 指向其他 Recommendations，§1.3 把 mechanical characteristics 指向 ISO/IEC 文献；因此此页不是 TIA-232 全文、连接器规范或完整上层通信协议。[SRC-001，pp. 1–2](sources.md#src-001)。

IBM 1984 年手册的外置 modem 例子可以帮助理解角色：DTE 是通信使用的信息处理设备，DCE 连接 DTE 与通信线路。IBM 使用历史称呼 **data communications equipment**；本页引用的 V.24 标题使用 **data circuit-terminating equipment**。保留各自措辞，不把两个版本当成同一份文本。[SRC-002，p. 8-3](sources.md#src-002)；[SRC-001，标题、§1.1](sources.md#src-001)。

## 角色视角

下表是 **V.24 的 circuit number，不是 connector contact number**。方向沿该 Recommendation 的 DTE/DCE 视角；短释义不代替各节的条件和操作要求。

| Circuit | V.24 名称 | 方向 | 本期怎样读 |
|---|---|---|---|
| 103 | Transmitted data | DTE → DCE | DTE 提供给 DCE 的数据；§3.5 |
| 104 | Received data | DCE → DTE | DCE 提供给 DTE 的数据；§3.6 |
| 105 | Request to send | DTE → DCE | 控制 DCE 的 data-channel transmit function；§3.7 |
| 106 | Ready for sending | DCE → DTE | DCE 是否准备接受 DTE 的数据；§3.8 |
| 107 | Data set ready | DCE → DTE | DCE 工作状态；含测试等条件，不能简化成“远端收到字节”；§3.9 |
| 108/2 | Data terminal ready | DTE → DCE | DTE 状态；其 ON 不单独保证 DCE 已接通线路；§3.11 |
| 109 | Data channel received line signal detector | DCE → DTE | 接收线路信号是否处于相应要求范围内；§3.12 |

来源：[SRC-001，Table 1、§§3.5–3.12，pp. 3–7](sources.md#src-001)。例如 §3.11 明说 DCE 接入线路可能还需要其他条件；这里不把各个 ready 信号拼成唯一通用握手顺序。

IBM p. 8-4 把 **Request to Send、Clear to Send、Data Set Ready、Data Terminal Ready** 分别对应到 105、106、107、108.2。常见缩写 RTS/CTS/DSR/DTR 可据此与 IBM 主机页对读，但要注意 IBM 的 **Clear to Send** 与这里 V.24 的 **Ready for sending** 是来源各自的名称。[SRC-002，p. 8-4](sources.md#src-002)。

### 检查自己的视角

如果你站在 DCE 一侧读到 circuit 103 的 “Transmitted data”，数据仍是**进入 DCE**，不会因你换了观察位置就变成 DCE 的输出。仅有一个设备标签“TX”还缺角色、设备手册和映射证据；不能从上表推导实际连线。[SRC-001，§§3.5–3.6](sources.md#src-001)；[接线前检查表](../../docs/HARDWARE-SAFETY.md)。

## 控制线路不是字节中的几个附加位

V.24 Table 1 将 103/104 列入 data 类，把 105/106 等列入 control 类。TI 对 PC 实现的介绍则把并串转换、start/stop bits 和 parity 的生成/检查放在 UART/ACE 一侧。两份资料共同帮助我们分开 **UART framing** 与 **独立控制 circuits**，但没有因此定义所有串口的帧格式。[SRC-001，Table 1，p. 3](sources.md#src-001)；[SRC-003，p. 1](sources.md#src-003)。

V.24 §1.1 说明实际设备会按应用从 circuits 中选择；§4.5 还讨论未实现的可选 circuits。故不能声称每台设备都使用全部控制信号，也不能把缺少控制线路的某台设备当成整个家族的规则。[SRC-001，pp. 1–2、17](sources.md#src-001)。

## 为什么接下来读 BIOS

在 IBM 的发送例程里，软件先设置 DTR/RTS，等待 DSR/CTS，再等待发送控制器就绪，最后写入待发字符。控制与数据的分工在软件清单中有独立位置。这是 **IBM 的这段实现**，不是从 V.24 七行摘要推出来的通用算法。[SRC-002，p. 5-52，listing lines 1698–1727](sources.md#src-002)。

完整 framing/timing、同步模式、数据流控协议和标准版本变化仍未完成；本页不发布速率/吞吐量换算或 null-modem 配线。继续阅读[IBM 主机路径](host-integration.md)，或者返回[展品总览](README.md)。
