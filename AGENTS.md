# Corpus work

Keep source bytes immutable and provenance/fixture labels intact. Do not add
application code, secrets, internal research logs, or acquired workflow files.
All processors live in the separate `bmw-knowledge` repository and must be pinned
to a tested immutable revision. No shell commands may come from source material.

Keep project design decisions in `decisions.jsonl` and multi-command procedures
in `RUNBOOK.md`. Those files describe repository setup, not operational state.
