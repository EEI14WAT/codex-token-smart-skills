# Codex Token Smart Skills

让你的 Codex 在开始任务、测试验证和多 skill 协作时更聪明、更省 token。

This repository contains three lightweight Codex skills for safer task starts, cheaper validation, and scoped multi-skill workflows.

## Skills

### `codex-task-gate`

Use before starting a task to quickly judge task size, missing inputs, environment risk, and whether user confirmation is needed.

It helps Codex:

- avoid starting oversized or ambiguous tasks too early;
- check whether files, images, logs, templates, or pasted text are already available;
- keep pre-task communication short and natural;
- remember environment-route failures within the current task turn.

### `token-smart-test-plan`

Use when the user explicitly asks to test, verify, check, run QA, or perform acceptance testing.

It helps Codex:

- avoid jumping straight into expensive full tests;
- recommend a staged test level: smoke test, structure test, or full test;
- explain the recommended level in detail while keeping other levels brief;
- automatically fall back when local tools such as LibreOffice, Gradle, or visual renderers are unavailable.

### `token-smart-codex`

Use for token-aware Codex workflows across multiple steps or multiple skills.

It helps Codex:

- start with task gating;
- use staged test planning only when testing is explicitly requested;
- read external skills precisely instead of loading unnecessary reference material;
- end with a concise project state and failure memory.

## Directory Structure

```text
codex-task-gate/
  SKILL.md
  agents/openai.yaml

token-smart-test-plan/
  SKILL.md
  agents/openai.yaml

token-smart-codex/
  SKILL.md
  agents/openai.yaml
```

## Installation

Copy the skill folders you want into your local Codex skills directory:

```powershell
Copy-Item -Recurse .\codex-task-gate "$HOME\.codex\skills\codex-task-gate"
Copy-Item -Recurse .\token-smart-test-plan "$HOME\.codex\skills\token-smart-test-plan"
Copy-Item -Recurse .\token-smart-codex "$HOME\.codex\skills\token-smart-codex"
```

Then restart Codex so the skills are rediscovered.

## Usage

You can invoke the skills directly in prompts:

```text
$codex-task-gate 先判断这个任务的颗粒度、缺失材料和环境风险，不要直接开始执行。
$token-smart-test-plan 接下来我要测试，请先给我一个分级测试方案，不要直接开始测试。
$token-smart-codex 请用更省 token 但不降低质量的方式规划并执行这个任务。
```

Recommended order:

1. Use `codex-task-gate` before formal execution.
2. Use `token-smart-test-plan` only when testing or validation is explicitly requested.
3. Use the relevant business skill for the actual work.
4. Use `token-smart-codex` to keep multi-step work compact and scoped.

## License

MIT License. See [LICENSE](LICENSE).
