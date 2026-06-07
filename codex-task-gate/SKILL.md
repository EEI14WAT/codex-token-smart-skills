---
name: codex-task-gate
description: Use before starting a task to judge task size, missing inputs, environment risk, and whether a short confirmation is needed.
---

# Codex Task Gate

Run this first before formal execution.

## Output Style

Keep the gate result short:

- short judgment
- short question when needed
- short confirmation after the user answers

## Default Response Style

For normal gate responses, keep the answer under 200-350 Chinese characters.

Use natural short paragraphs instead of rigid field labels.

Default flow:

- first state in one sentence whether the task is too large or risky
- then give a complete but short milestone split
- then explain what to do in this turn and how it relates to the first milestone
- finally list at most 3 confirmation questions
- end by saying confirmation is needed before starting

Do not write a long report unless the user explicitly asks for detailed analysis.

For oversized tasks:

- list at most 5-6 milestones in one compact line when possible
- ask at most 3 key questions
- list at most 3 exclusions

For app or project generation tasks, the first recommended turn should usually start with the first milestone: project skeleton, basic build config, manifest, theme, and empty home screen, so the project can open, sync, or run before deeper features are added.

## Provided Materials Check

Before asking the user for missing inputs, first check whether the user has already provided them.

Look for:

- uploaded files or images
- pasted text
- screenshots
- error logs
- templates
- current working directory files
- user statements such as "我已经给了", "就在当前文件夹", "用这个文件", or "用已有文件"

Do not ask for materials that are already available.

If required material may already exist in the current folder, inspect the folder first. If the material may exist but the name is unclear, say briefly that you will first look for relevant files in the current folder instead of asking the user to upload again.

Only ask the user after confirming the material is unavailable or ambiguous.

When asking, ask at most 3 key questions and keep the gate response natural and short.

## Confirmation Rule

Ask for confirmation before starting when:

- task is medium or large
- task may require missing files, images, data, credentials, or links
- task may use expensive tools
- task may generate long documents or decks
- task may modify many files
- task may run tests
- task scope is ambiguous
- task depends on environment setup or external services

Do not ask for confirmation when:

- the user gives an explicit small bug fix
- all inputs are present
- the change is local and low risk
- the user explicitly says "直接做"
- the user asks for a clearly scoped single-file edit

## Routing Order

1. Use `codex-task-gate` to judge size, missing material, and environment risk.
2. If the user explicitly asks to test, verify, check, or run something, use `token-smart-test-plan`.
3. Execute the relevant business skill.
4. If another skill is needed during execution, read only the necessary fragment.
5. End with a brief project state and failure memory.

## Environment Failure Memory

If a tool or route fails once because the environment is missing, unavailable, or blocked, remember it for this task turn and do not retry the same route. Choose a cheaper alternate route or report the blocker briefly.
