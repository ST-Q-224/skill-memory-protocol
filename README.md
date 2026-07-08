# Skill Memory Protocol

**The complete instruction set: 4 groups, 8 operations.**

A protocol for capturing, querying, and monetizing expert skill memories — with verifiable rights enforcement and automatic revenue sharing back to the masters who contribute them.

## Instruction Set Overview

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

## The Four Groups

### 1. Supply Side — where value enters

- **`CAPTURE`** — The zeroth instruction. A master's multimodal work stream (video, audio, sensor data, annotations) is encoded into the memory store. Every write is compensated: encoding is not just ingestion, it is the origin of the revenue-share chain.
- **`REVOKE`** — Ownership stays with the master. When a master exits or a license expires, their memories are taken down in a *verifiable* way. Delisting is provable, not a promise.

### 2. Consume Side — where value is priced

- **`QUERY`** — Metered per call, in three subtypes:
  - **Retrieval** — find matching memories
  - **Decoding** — reconstruct a memory into usable guidance
  - **Evaluation** — score an attempt against stored expertise
- **`SUBSCRIBE`** — A standing query. Instead of asking repeatedly, a consumer subscribes: *"notify me when process X gains new memories."* Billed per period. This turns the "sell the delta" (newswire) business model into a protocol primitive.

### 3. Maintain Side — where the store stays coherent

- **`RESOLVE`** — Conflict resolution. Two masters may encode contradictory techniques for the same process. The skill domain makes this uniquely hard: conflicting memories can *both* be valid (different schools, different conditions). `RESOLVE` adjudicates, versions, or forks conflicting memories rather than silently overwriting.
- **`RECOMPILE`** — When the encoder is upgraded or a new modality is added, the entire store is re-encoded. Critically, this is a **re-licensing event** for buyers: a capability leap re-monetizes the existing stock, and the protocol makes that explicit rather than accidental.

### 4. Settle Side — where value flows back

- **`ATTRIBUTE`** — Provenance is mandatory. Every query response carries the list of contributing masters' memories. Attribution is the ground truth for payment.
- **`SETTLE`** — Revenue distribution runs automatically against attribution logs. No manual accounting; the split is a function of recorded provenance.

## Design Principles

1. **Writes are paid.** Supply-side compensation starts at `CAPTURE`, not at first sale.
2. **Rights are executable.** `REVOKE` makes exit verifiable, not contractual fine print.
3. **Every answer has a receipt.** `ATTRIBUTE` binds each response to its sources; `SETTLE` pays against those receipts.
4. **Upgrades re-monetize the archive.** `RECOMPILE` treats capability leaps as licensing events for existing stock.
5. **Conflict is a feature.** `RESOLVE` preserves competing schools of technique instead of flattening them.
