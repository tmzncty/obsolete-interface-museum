# Research lead: Z-Link / Gen-Z 4C 识别与 storage-interface terminology 种子

- **日期**：2026-10-01（线索来自 2026-09-27 备份对话「解释奇怪接口」，Amphenol 官方资料核验）
- **性质**：按 ROADMAP 的 research-first 流程立线索，不直接建展品
- **证据等级**：对话内已带安费诺官方来源（Z-Link 1C/2C/4C/4C+ 规格、SFF-TA-1002），编纂时需重新核链+快照

## 线索一：SFF-TA-1002 / Amphenol ExtremePort Z-Link（Gen-Z 4C）

服务器内「搬 PCIe 高速信号」的连接器族。核心识别点：**4C = 140 pin = 32 对高速差分线 = PCIe x16（16TX+16RX）**，可跑 PCIe Gen5；1C=8 对、2C=16 对（chiclet=高速通道单元）。存在动机：PCIe 5.0 32GT/s 下 PCB 长走线的插损/串扰/过孔/FR-4 损耗失控——**尽早钻进 Twinax 线缆**（CPU→短 PCB→Z-Link→Twinax→PCIe slot）。同族：MCIO / SlimSAS / OCuLink / Z-Link / Near-Chip Connector / OverPass——共同趋势：**PCIe 从主板铜箔总线变成机箱内高速串行布线系统**。命名陷阱：Z-Link 深植 Gen-Z 生态但 SFF-TA-1002 连接器不必然承载 Gen-Z 协议（多为 PCIe/NVMe）。

**展品建议**：与 ROADMAP 规划的 `research/storage-interface-terminology.md` 分开立线（那是 ATA/IDE/PATA/SCSI/SAS 层次辨析；这是 PCIe cabling 族）——候选名 `pci-express-cabling`，覆盖 OCuLink→MCIO→SlimSAS→Z-Link 演化。

## 线索二：SATA 与 SAS 区别的术语种子（09-20 备份对话）

对话覆盖点（供未来 terminology 文档引用）：SAS=SCSI 协议族、双端口、扩展器拓扑、企业 TLER/振动规格 vs SATA=ATA 族单端口消费级；协议分层上 SATA 可桥接于 SAS 控制器而反之不行。此线按 ROADMAP 原计划先建 terminology 文档，对话内容仅作种子。

## 本文件不处理

「识别风扇型号」（非接口）、「确认四口 50G 网卡 / 核对硬件规格 / 分析显卡型号」（个人硬件核对）已归 catgirl-archive。
