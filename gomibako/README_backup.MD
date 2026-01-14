IME Persona Patch

Personalized input, without changing your IME.

IME learns who you are,
without ever seeing what you type.

What is this?

IME Persona Patch is an experimental system that adds a personalization layer on top of existing IMEs
(Google Japanese Input / Mozc, etc.), without modifying them.

It does not try to replace your IME.
It quietly augments it.

No new keyboard

No OS-level replacement

No cloud dependency required

Just a thin, local “persona patch” between your thoughts and your input.

Motivation

Modern IMEs are extremely good at:

general language correctness

new words and trends

average user behavior

But they are still very bad at:

your metaphors

your recurring explanations

your way of hesitating, rephrasing, or simplifying

long-term personal context

Meanwhile:

LLMs remember context

RAG remembers knowledge

IME still forgets you

This project explores a simple question:

What if an IME could have a personality,
without becoming intrusive or surveillance-based?

Core Idea

Instead of training a new IME from scratch, we:

Observe how you revise, rephrase, and reuse expressions

Distill only the high-confidence “surface layer” of your thinking

Promote that layer into your IME user dictionary

Do it locally, quietly, and reversibly

Think of it as:

RAG → skimming → IME

knowledge → expression → habit

What this is not

❌ Not a replacement IME

❌ Not a cloud learning system

❌ Not a keystroke logger

❌ Not an auto-completion spammer

This project explicitly avoids:

full text storage

aggressive prediction

UI noise

model retraining at the IME level

Architecture (High Level)
Speech / Text / Edits
        ↓
   Python Core
 (RAG + embeddings)
        ↓
   Go Filter
 (skimming & decay)
        ↓
  Java IME Bridge
 (user dictionary sync)
        ↓
 Existing IME

Language Roles

Python
RAG, embeddings, expression extraction, bias modeling

Go
Fast filtering, time decay, promotion thresholds

Java
User dictionary integration (Mozc / Google IME / Android IME)

TypeScript
UI for visibility, control, and demos

What gets promoted to the IME?

Not raw words.

Only expressions that are:

reused over time

stable (not frequently edited)

short, expressive, and reusable

clearly “you”

Examples:

definitions you keep explaining the same way

metaphors you naturally reuse

sentence starters you trust

Speech Recognition (Optional)

Speech recognition is treated as input hypotheses, not truth.

Generic ASR (Google / Whisper) → 70% accuracy is enough

Personal bias is applied after recognition

Corrections are learning signals

Silence and hesitation are signals too

We optimize how it misunderstands you, not raw accuracy.

Privacy & Philosophy

Local-first by default

No mandatory cloud sync

No behavioral scoring

No “learning notifications”

Learning should feel invisible.

If the system makes you self-conscious, it’s broken.

Why a “Patch”?

IME is one of the most latency-sensitive, platform-dependent components in computing.

Replacing it is unrealistic.
Extending it is respectful.

This project treats IME as:

a sacred final layer
that should be enhanced, not disrupted.

Status

🚧 Experimental / Research-grade
Currently focused on:

personal RAG distillation

dictionary promotion heuristics

Mozc / Google IME user dictionary workflows

Who is this for?

Developers with strong personal writing habits

Researchers exploring personalization without surveillance

IME / HCI / NLP engineers

Anyone who feels their tools are smart, but not familiar

License

TBD (likely Apache-2.0 or MIT)

One-line Summary

IME Persona Patch explores how input methods can adapt to individuals
without retraining models, replacing keyboards, or sending data to the cloud.
