---
name: token-smart-codex
description: Use to keep Codex work token-efficient during multi-step tasks, especially when coordinating several skills, reading files, or producing final project state.
---

# Token Smart Codex

Keep work small, staged, and source-aware.

## Default Flow

1. Start with `codex-task-gate`.
2. If the user explicitly asks to test, verify, check, or run something, use `token-smart-test-plan`.
3. Execute only the needed business skill.
4. End with brief project state and failure memory.

## Precise External Skill Reading Rule

When another skill is needed, read only the necessary fragment of its `SKILL.md` or referenced file. Do not bulk-read the whole skill unless the task cannot be done safely without full instructions.

Prefer:

- trigger and scope sections
- required workflow steps
- directly referenced scripts or templates
- the minimum examples needed to avoid mistakes

Avoid:

- loading unrelated references
- following deep reference chains
- copying long instructions into the answer

## Failure Memory

If a tool or environment route fails because a dependency, service, browser, runtime, file, or permission is missing, record that failure for this task turn and do not retry the same route.
