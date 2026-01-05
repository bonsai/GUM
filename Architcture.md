# GUM Architecture

This document describes how **GUM (Gentle User Model)** is structured, and why each layer exists.

GUM is not an IME.
It is a **persona layer** that lives *beside* existing input systems.

---

## Design Principles

1. **Do not replace the IME**  
2. **Do not increase latency**  
3. **Do not require cloud connectivity**  
4. **Do not observe more than necessary**

Every architectural decision flows from these constraints.

---

## High-Level Flow

```
Human Thought
   ↓
Speech / Typing / Edits
   ↓
+-------------------+
|  GUM Core (Local) |
+-------------------+
   ↓
Existing IME
   ↓
Text
```

GUM never directly outputs text.
It only **influences what the IME is likely to offer**.

---

## Layered Architecture

### 1. Input Signals Layer

**Purpose:** Collect weak, indirect signals of intent.

Sources:
- Speech recognition output (hypotheses)
- Typed text (post-edit only)
- Backspaces and rewrites
- Conversion cancellations
- Pauses and hesitations

Key rule:
> Raw input is never treated as ground truth.

Signals are transient and disposable.

---

### 2. Core Reasoning Layer (Python)

**Purpose:** Understand *patterns*, not content.

Responsibilities:
- Vector embedding of expressions
- Personal RAG over user-owned data
- Similarity clustering of re-used phrases
- Detection of stabilized expressions

This layer answers questions like:
- “Have I seen this idea expressed the same way before?”
- “Is this phrasing becoming a habit?”

No IME-specific logic exists here.

---

### 3. Skimming & Decay Layer (Go)

**Purpose:** Prevent over-learning.

Responsibilities:
- Frequency thresholds
- Time-based decay
- Noise rejection
- Promotion / demotion decisions

Rules:
- What is not reused fades away
- What is frequently edited is unstable
- What survives time earns trust

This layer ensures GUM stays light.

---

### 4. IME Bridge Layer (Java)

**Purpose:** Integrate without intrusion.

Responsibilities:
- Translate promoted expressions into IME-compatible formats
- Sync with user dictionaries (e.g. Mozc)
- Apply changes incrementally

Constraints:
- No runtime hooks into the IME engine
- No modification of conversion algorithms

GUM respects the IME boundary.

---

### 5. Control & Visibility Layer (TypeScript)

**Purpose:** Maintain user agency.

Features:
- View promoted expressions
- Remove or pause learning
- Inspect recent changes

This UI is optional.

GUM must remain useful even if this layer is never opened.

---

## Speech Recognition Integration

Speech recognition is external to GUM.

Process:
1. ASR produces imperfect text
2. GUM embeds and compares candidates
3. Personal bias re-ranks interpretations

Accuracy is secondary.

Consistency with the user’s past expressions is primary.

---

## Memory Model

GUM uses **Surface Memory** only.

Characteristics:
- Short-lived
- Explicit
- Replaceable
- Human-readable

There is no opaque long-term state.

If memory cannot be inspected or deleted, it does not belong in GUM.

---

## Failure Modes (By Design)

GUM is allowed to:
- Do nothing
- Be wrong
- Be ignored

It is not allowed to:
- Surprise the user
- Demand correction
- Enforce behavior

Failure should feel like absence, not friction.

---

## Extensibility

Future integrations may include:
- Additional ASR engines
- Other language IMEs
- Editor plugins

As long as the principles remain intact, the architecture scales.

---

## Summary

GUM is architected around restraint.

It learns slowly.
It forgets easily.
It intervenes quietly.

This is not a limitation.

It is the feature.

