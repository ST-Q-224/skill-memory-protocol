# Skill Memory Protocol · 技能记忆协议

[English](#english) | [简体中文](#简体中文)

---

## English

**The complete instruction set: 4 groups, 8 operations.**

A protocol for capturing, querying, and monetizing expert skill memories — with verifiable rights enforcement and automatic revenue sharing back to the masters who contribute them.

### Instruction Set Overview

| Group | Operation | Semantics | Billing / Direction |
|---|---|---|---|
| **Supply side** | `CAPTURE` | Multimodal stream → encoded and written to the memory store | Pay the master per encoding — writing is the supply-side operation and the starting point of revenue share |
| **Supply side** | `REVOKE` | Master exits / license expires → memory is verifiably delisted | Rights enforcement |
| **Consume side** | `QUERY` | Three subtypes: retrieval, decoding, evaluation | Pay per call |
| **Consume side** | `SUBSCRIBE` | Standing query: "push me when process X gains new memories" | Pay per period — the "sell-the-delta / newswire" model, protocolized |
| **Maintain side** | `RESOLVE` | Conflict resolution — the most distinctive operation in the skill domain (see below) | Internal |
| **Maintain side** | `RECOMPILE` | Encoder upgrade / new modality added → full re-encoding of the store | A re-licensing event for buyers — "capability leaps re-monetize existing stock," protocolized |
| **Settle side** | `ATTRIBUTE` | Every query result carries its provenance: which masters' memories contributed to the answer | Basis for revenue split |
| **Settle side** | `SETTLE` | Distribute revenue to the supply side according to attribution logs | Automatic revenue sharing |

### The Four Groups

#### 1. Supply Side — where value enters

- **`CAPTURE`** — The zeroth instruction. A master's multimodal work stream (video, audio, sensor data, annotations) is encoded into the memory store. Every write is compensated: encoding is not just ingestion, it is the origin of the revenue-share chain.
- **`REVOKE`** — Ownership stays with the master. When a master exits or a license expires, their memories are taken down in a *verifiable* way. Delisting is provable, not a promise.

#### 2. Consume Side — where value is priced

- **`QUERY`** — Metered per call, in three subtypes:
  - **Retrieval** — find matching memories
  - **Decoding** — reconstruct a memory into usable guidance
  - **Evaluation** — score an attempt against stored expertise
- **`SUBSCRIBE`** — A standing query. Instead of asking repeatedly, a consumer subscribes: *"notify me when process X gains new memories."* Billed per period. This turns the "sell the delta" (newswire) business model into a protocol primitive.

#### 3. Maintain Side — where the store stays coherent

- **`RESOLVE`** — Conflict resolution. Two masters may encode contradictory techniques for the same process. The skill domain makes this uniquely hard: conflicting memories can *both* be valid (different schools, different conditions). `RESOLVE` adjudicates, versions, or forks conflicting memories rather than silently overwriting.
- **`RECOMPILE`** — When the encoder is upgraded or a new modality is added, the entire store is re-encoded. Critically, this is a **re-licensing event** for buyers: a capability leap re-monetizes the existing stock, and the protocol makes that explicit rather than accidental.

#### 4. Settle Side — where value flows back

- **`ATTRIBUTE`** — Provenance is mandatory. Every query response carries the list of contributing masters' memories. Attribution is the ground truth for payment.
- **`SETTLE`** — Revenue distribution runs automatically against attribution logs. No manual accounting; the split is a function of recorded provenance.

### Design Principles

1. **Writes are paid.** Supply-side compensation starts at `CAPTURE`, not at first sale.
2. **Rights are executable.** `REVOKE` makes exit verifiable, not contractual fine print.
3. **Every answer has a receipt.** `ATTRIBUTE` binds each response to its sources; `SETTLE` pays against those receipts.
4. **Upgrades re-monetize the archive.** `RECOMPILE` treats capability leaps as licensing events for existing stock.
5. **Conflict is a feature.** `RESOLVE` preserves competing schools of technique instead of flattening them.

---

## 简体中文

**完整指令集：四组八条。**

一个用于采集、查询并变现专家技能记忆的协议——具备可验证的权利执行机制，并向贡献记忆的师傅自动分成。

### 指令集总览

| 组 | 操作 | 语义 | 计费方向 |
|---|---|---|---|
| **供给侧** | `CAPTURE`（采集编码） | 多模态流 → 编码入库 | 一次编码向师傅付——写入是供给方的操作，也是分成的起点 |
| **供给侧** | `REVOKE`（撤回） | 师傅退出 / 授权到期 → 记忆可验证下架 | 权利执行 |
| **消费侧** | `QUERY`（查询） | 检索式 / 解码式 / 评估式三种子类型 | 按次收 |
| **消费侧** | `SUBSCRIBE`（订阅） | 站桩查询："X 工艺有新记忆时推给我" | 按期收——"卖 Δ / 通讯社"模式的协议化 |
| **维护侧** | `RESOLVE`（冲突解决） | 技能域最特殊的一条（见下） | 内部 |
| **维护侧** | `RECOMPILE`（更新内核） | 编码器升级 / 新模态加入 → 全库重编码 | 对买方是再授权事件——"能力跃迁重新变现存量"的协议化 |
| **结算侧** | `ATTRIBUTE`（溯源） | 每次查询结果携带贡献来源：哪些师傅的记忆参与了应答 | 分账依据 |
| **结算侧** | `SETTLE`（结算） | 按溯源日志向供给侧分成 | 自动分账 |

### 四组详解

#### 一、供给侧——价值的入口

- **`CAPTURE`（采集编码）**——第 0 条指令。师傅的多模态工作流（视频、音频、传感器数据、标注）被编码写入记忆库。每次写入都获得报酬：编码不只是数据摄入，而是分成链条的起点。
- **`REVOKE`（撤回）**——所有权始终归师傅。师傅退出或授权到期时，其记忆以*可验证*的方式下架。下架是可证明的，不是一句承诺。

#### 二、消费侧——价值的定价

- **`QUERY`（查询）**——按次计费，三种子类型：
  - **检索式**——找到匹配的记忆
  - **解码式**——把记忆还原为可用的操作指导
  - **评估式**——用库存专家经验为一次操作打分
- **`SUBSCRIBE`（订阅）**——站桩查询。消费者不必反复询问，而是订阅："X 工艺有新记忆时推给我。"按期计费。这把"卖 Δ"（通讯社）商业模式变成了协议原语。

#### 三、维护侧——保持库的一致性

- **`RESOLVE`（冲突解决）**——两位师傅可能对同一工艺编码出相互矛盾的技法。技能域的特殊之处在于：冲突的记忆可能*都*是对的（不同流派、不同工况）。`RESOLVE` 对冲突记忆做裁决、版本化或分叉，而不是悄悄覆盖。
- **`RECOMPILE`（更新内核）**——编码器升级或新模态加入时，全库重编码。关键在于：这对买方是一次**再授权事件**——能力跃迁重新变现存量，协议将其显式化，而非任其偶然发生。

#### 四、结算侧——价值的回流

- **`ATTRIBUTE`（溯源）**——溯源是强制的。每次查询应答都携带参与贡献的师傅记忆清单。溯源即分账的事实依据。
- **`SETTLE`（结算）**——按溯源日志自动执行分成。无需人工对账，分成是记录在案的溯源数据的函数。

### 设计原则

1. **写入即有偿。** 供给侧报酬从 `CAPTURE` 开始，而不是从第一笔销售开始。
2. **权利可执行。** `REVOKE` 让退出可验证，而非合同里的小字。
3. **每个答案都有收据。** `ATTRIBUTE` 把每次应答绑定到来源，`SETTLE` 凭收据付款。
4. **升级重新变现存量。** `RECOMPILE` 把能力跃迁视为对存量的再授权事件。
5. **冲突是特性。** `RESOLVE` 保留相互竞争的技法流派，而不是把它们抹平。
