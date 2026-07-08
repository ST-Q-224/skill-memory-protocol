# Pricing Model · 数据分级定价

[English](#english) | [简体中文](#简体中文)

---

## English

**One axiom: value ∝ rarity × decision content.**

A memory that any junior operator could produce is worth little. A memory that encodes how a 30-year master handled a once-a-year failure is worth orders of magnitude more. The protocol prices this explicitly instead of averaging it away.

### The Two Pricing Dimensions

| Dimension | Symbol | What it measures | How it is estimated (v0) |
| --------- | ------ | ---------------- | ------------------------ |
| **Rarity** | `R` | How scarce this memory is in the store: how many masters, across how many sites, have encoded memories covering the same process state | Inverse coverage count within a process cluster, normalized to [1, R_max] |
| **Decision content** | `D` | How much judgment the memory encodes: branching, trade-offs, irreversible choices — versus rote procedure | Ratio of decision points to total steps in the encoded trace, normalized to [1, D_max] |

**Unit price of a memory:**

```
P = P_base × R × D
```

`P_base` is the floor price of a routine, fully-covered memory. `R` and `D` are multipliers ≥ 1. Both are computed at `CAPTURE` time and re-computed at `RECOMPILE`.

### The Four Tiers

Routine vs. exceptional is not binary — it is a ladder. v0 defines four tiers:

| Tier | Name | Typical content | R × D range (indicative) |
| ---- | ---- | --------------- | ------------------------ |
| **T0** | Routine operation | Standard procedure under normal conditions; many masters encode near-identical memories | 1× (floor) |
| **T1** | Parameter judgment | Tuning, adaptation to material/tool/ambient variation; moderate coverage, real judgment | 2–5× |
| **T2** | Exception handling | Fault diagnosis and recovery; few masters have seen the failure, decisions are consequential | 5–20× |
| **T3** | Incident response | Rare, high-stakes saves: the once-a-year failure, the "call the old master at 2 a.m." case | 20×+ , price largely set by scarcity auction / negotiation |

Tier assignment is a *pricing label*, not a separate mechanism: it is the banded output of `R × D`.

### How Pricing Binds to the Instruction Set

| Instruction | Pricing behavior |
| ----------- | ---------------- |
| `CAPTURE` | Supply-side payment scales with tier. T0 writes earn the floor rate; T2/T3 writes earn multiples. This is what makes masters *want* to encode their exception cases instead of hoarding them. |
| `QUERY` | Per-call price = sum of contributing memories' `P`, weighted by attribution share. Retrieval < decoding < evaluation in per-call coefficient. |
| `SUBSCRIBE` | Priced per period, with a tier filter: a subscription to "T2+ deltas on process X" costs more than "all deltas," because the delta stream's value is concentrated in exceptions. |
| `RECOMPILE` | Re-licensing event: all `R` and `D` values are re-computed under the new encoder; buyers re-license at the new prices. Capability leaps re-monetize the archive. |
| `ATTRIBUTE` / `SETTLE` | Revenue splits use price-weighted attribution: a T3 memory contributing 10% of an answer earns more than a T0 memory contributing 50%. |

### Anti-Gaming (v0 placeholders)

- **Duplicate flooding:** near-duplicate captures collapse into one memory with shared ownership; flooding raises coverage and *lowers* your own `R`.
- **Fake exceptions:** T2/T3 labels require corroborating evidence in the trace (alarm logs, sensor excursions, downstream confirmation). Uncorroborated exception claims settle at T1.
- **Decay:** `R` is recomputed as coverage grows. Early encoders of a process enjoy high `R` that decays as the store fills — first movers are rewarded, monopolies are not permanent.

### Open Questions (tracked, not solved in v0)

1. Cross-site rarity: is a memory rare globally or only within one factory?
2. `D` estimation without a mature decision-point extractor — v0 may use human labeling.
3. Price floors for masters vs. price discovery for buyers: where does negotiation live in the protocol?

---

## 简体中文

**一条公理：价值 ∝ 稀有度 × 决策含量。**

任何新手都能产出的记忆不值钱；编码了三十年老师傅处理"一年一遇故障"的记忆,贵一个数量级以上。协议把这件事显式定价,而不是用均价抹平。

### 两个定价维度

| 维度 | 符号 | 度量什么 | v0 估计方法 |
| ---- | ---- | -------- | ----------- |
| **稀有度** | `R` | 该记忆在库中的稀缺程度:同一工艺状态下,有多少位师傅、多少个现场编码过覆盖性记忆 | 工艺簇内覆盖数的倒数,归一化到 [1, R_max] |
| **决策含量** | `D` | 记忆中编码了多少判断:分支、取舍、不可逆选择——相对于照章操作 | 编码轨迹中决策点与总步骤之比,归一化到 [1, D_max] |

**单条记忆的单价:**

```
P = P_base × R × D
```

`P_base` 是常规、全覆盖记忆的地板价。`R`、`D` 为 ≥1 的乘数,在 `CAPTURE` 时计算,`RECOMPILE` 时重算。

### 四级分级

常规/异常不是二分,是阶梯。v0 定义四级:

| 级别 | 名称 | 典型内容 | R × D 区间(示意) |
| ---- | ---- | -------- | ------------------ |
| **T0** | 常规操作 | 正常工况下的标准流程;多位师傅的记忆几乎相同 | 1×(地板价) |
| **T1** | 参数判断 | 调参、对材料/刀具/环境波动的适应;覆盖中等,有真实判断 | 2–5× |
| **T2** | 异常处置 | 故障诊断与恢复;见过该故障的师傅很少,决策后果重大 | 5–20× |
| **T3** | 事故救火 | 一年一遇的高风险抢救、"凌晨两点打电话请老师傅"的场景 | 20× 起,价格主要由稀缺竞价/协商决定 |

分级是**定价标签**,不是独立机制:它就是 `R × D` 的分段输出。

### 定价如何绑定到指令集

| 指令 | 定价行为 |
| ---- | -------- |
| `CAPTURE` | 供给侧报酬随级别放大:T0 写入拿地板价,T2/T3 写入拿数倍。这是让师傅**愿意**编码异常案例而不是藏着掖着的原因。 |
| `QUERY` | 单次价格 = 参与应答的记忆的 `P` 按溯源权重求和;检索式 < 解码式 < 评估式的调用系数依次递增。 |
| `SUBSCRIBE` | 按期计费,带级别过滤:订阅"X 工艺 T2 以上的增量"比订阅"全部增量"更贵——增量流的价值集中在异常里。 |
| `RECOMPILE` | 再授权事件:新编码器下全库 `R`、`D` 重算,买方按新价再授权。能力跃迁重新变现存量。 |
| `ATTRIBUTE` / `SETTLE` | 分账按价格加权溯源:贡献了应答 10% 的 T3 记忆,分成多于贡献 50% 的 T0 记忆。 |

### 防博弈(v0 占位)

- **灌水刷量:** 近似重复的采集合并为一条共有记忆;灌水推高覆盖数,反而**压低**自己的 `R`。
- **伪造异常:** T2/T3 标签要求轨迹中有佐证(报警日志、传感器越限、下游确认)。无佐证的异常主张按 T1 结算。
- **衰减:** `R` 随覆盖增长重算。某工艺的早期编码者享受高 `R`,随库存填满而衰减——奖励先行者,但垄断不永久。

### 未决问题(记录,v0 不解)

1. 跨现场稀有度:一条记忆是全局稀有,还是只在某一家工厂稀有?
2. 没有成熟决策点抽取器时如何估 `D`——v0 可能用人工标注。
3. 师傅的保底价 vs 买方的价格发现:协商在协议中的位置在哪?
