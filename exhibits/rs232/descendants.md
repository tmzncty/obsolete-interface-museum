# 后继与替代：先保留问题，不制造关系

[展品总览](README.md) · [来源账本](sources.md) · [关系词定义](../../docs/RELATIONSHIPS.md)

## 本期没有已确认的关系记录

`exhibit.json` 的 `relationships` 为空。这不表示 RS-232 没有后继、适配器或继续使用的场景；只表示本期亲读的材料尚不足以建立这里所需的、具有 layer/scope/requires/evidence 的具体关系边。

## 已有的两个历史窗口

IBM 1984 手册 pp. 8-3–8-5 用 DTE、外置 modem 与通信线路解释连接；TI 2002 年应用笔记 p. 1 列举 PC 及多类外围设备的 232 应用。这能支持“阅读材料中的使用语境不止一种”，却不能单凭这两份文献确定该接口何时全面退出主流，或哪种接口在所有场景中取代了它。[SRC-002](sources.md#src-002)；[SRC-003](sources.md#src-003)。

## 下一份证据应回答什么

| 待研究问题 | 必须限定的层与范围 |
|---|---|
| 某类 modem 或外设改用什么接口？ | `ecosystem`：具体设备类别、年代和使用场景；不是电气兼容声明 |
| 某个 adapter 能保留哪些行为？ | 指定产品、bridge/transceiver、driver 与 signals；不能把 USB 适配器当成一根无条件透明的线 |
| 软件接口或控制语义保留了什么？ | `host` / `protocol`：应有对应版本/实现文档，不能仅凭相似名称 |
| 相似外壳能否互连？ | `physical` 相似与 `electrical` / `protocol` 互操作分别取证，并遵守硬件门禁 |

这些是研究问题，不是本页宣布的兼容、替代或继承事实。暂不写“USB 直接替代 RS-232”、未选定产品的通用能力、或不带年代的衰退结论。

填入具体关系前应满足[关系词契约](../../docs/RELATIONSHIPS.md)与[证据规则](../../docs/EVIDENCE.md)；原资料地图中关于 adapter、null modem 与标准版本的未知项仍然保留。

[返回展品总览](README.md)
