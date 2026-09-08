# IBM 1984 个案：软件怎样看到“串口”

[展品总览](README.md) · 上一站：[角色与控制](protocol.md) · 下一站：[电气边界](electrical.md)

## 先限定机器与来源

本页阅读 IBM *Personal Computer Technical Reference*，**Revised Edition, April 1984，publication 6361453**。下文是该 IBM PC/5150 文献中的 BIOS/8250 个案；不是现代 tty/COM 驱动教程，也不声称后来的兼容机或 USB 适配器使用同一路径。页码均是书内印刷页码。[SRC-002](sources.md#src-002)。

## 三种不要混在一起的地址与状态

| 文献中的对象 | 在这个实现里是什么 | 去哪里看 |
|---|---|---|
| 内存位置 `400h–407h` | 保存已连接 RS-232C 卡的 base addresses 的 BIOS 数据区 | p. 5-8 |
| `RS232_BASE` / 8250 base address | 例程据此定位卡上的控制器寄存器；不是 connector contact 编号 | p. 5-51，lines 1608–1609、1639–1645 |
| `INT 14h` 的 `AH`/`AL` | 调用参数或返回结果；状态请求返回 line / modem 两组状态 | pp. 5-50–5-51、5-53 |

以上均据 [SRC-002](sources.md#src-002)。本文只解释清单，不让读者在当前机器上执行端口写入。

## 四个 BIOS 服务

IBM 的清单按调用时的 `AH` 区分四类操作：[SRC-002，pp. 5-50–5-51，lines 1551–1604](sources.md#src-002)。

| 调用时 AH | 清单描述的操作 | 阅读重点 |
|---|---|---|
| 0 | 初始化通信端口，`AL` 给出配置参数 | 参数中分别有速率选择、parity、stop bit、word length；这不是整条线路的有效吞吐量报告 |
| 1 | 发送 `AL` 中的字符 | 该路径包含控制状态等待和超时处理，见下节 |
| 2 | 接收字符到 `AL` | 接收路径返回状态/错误信息；没有在本展品中实际运行 |
| 3 | 返回通信端口状态到 `AX` | `AH` 是 line status，`AL` 是 modem status |

例如，IBM 将 framing/parity/overrun 等列在线状态注释中，将 CTS/DSR/ring/received-line-signal 等列在 modem 状态注释中。这是**软件可见的状态划分**，不表示程序直接测量了电压或观察了线缆内部。[SRC-002，p. 5-51，lines 1586–1604；p. 5-53，lines 1753–1762](sources.md#src-002)。

## 沿一次发送请求读清单

这是文献导读，**不是已执行的 trace，也不是接线/操作步骤**。在卡的 base address 有效并进入发送分支的前提下，可按下列顺序查阅原清单：

```text
INT 14h 的发送请求（AH=1，AL 为字符）
        ↓
按 RS232_BASE 定位 8250 寄存器
        ↓
modem control：设置 DTR 与 RTS
        ↓
modem status：等待 DSR 与 CTS；未满足可超时返回
        ↓
line status：等待发送 holding register 就绪；未满足可超时返回
        ↓
把字符写入 data port，返回调用者
```

来源：[SRC-002，p. 5-51，lines 1639–1649；p. 5-52，lines 1698–1727；p. 5-53，lines 1763–1789](sources.md#src-002)。`WAIT_FOR_STATUS` 用状态读取与计数循环判断成功/超时；图中没有规定一个通用的毫秒数，也没有给出远端接收确认。

对照[角色页](protocol.md)能看出：DTR/RTS 是这个 DTE 侧提出的控制状态，DSR/CTS 则是从 DCE 侧观察的状态。IBM 在 modem 图中使用这些名称和 circuit 对应；例程如何等待它们，应回到 IBM 清单核验，而不是假定所有驱动都做同样的等待。[SRC-002，pp. 8-3–8-4、5-52](sources.md#src-002)。

### 一个失败分支能教会什么

这段发送例程在等到所需 modem status **之前**不会走到写字符的分支；超时路径会设置返回状态中的超时位。因此，“程序没有成功发出字符”的阅读问题不能只查字节格式，还要查这段实现要求的控制状态。

这是对已印刷代码的解释，不是对某根现有电缆的诊断，更不说明应短接任何控制线路。[SRC-002，p. 5-52，lines 1702–1727](sources.md#src-002)。

## 这个切片没有证明什么

- 没有实际启动 BIOS、模拟器或硬件；没有 E3/E4 结果。
- 没有为现代 OS 的发现、驱动、tty/COM API 或特定 USB bridge 建立来源，不能从本页推断其行为。
- 没有覆盖 IRQ/DMA 配置史、全部兼容机、应用层重试或 modem 指令集。
- BIOS 状态和 UART 寄存器不决定 connector mapping、允许电压、热插拔或真实线缆安全性。

继续阅读[电气边界](electrical.md)与[物理边界](physical.md)，在[实验页](experiment.md)查看未满足的条件；[返回展品总览](README.md)。
