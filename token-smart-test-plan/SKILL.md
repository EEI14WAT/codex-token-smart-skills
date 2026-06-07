---
name: token-smart-test-plan
description: Use when the user explicitly asks to test, verify, check, run QA, run an acceptance test, 测试, 验证, 检查, 跑一下, QA, or 验收; propose a token-saving test plan before expensive execution.
---

# Token Smart Test Plan

Use only when the user explicitly asks for testing or verification, such as "测试", "验证", "检查", "跑一下", "QA", "验收", "test", "verify", "check", "run QA", or "acceptance test".

Do not use this skill for normal task gating. Task size, missing materials, and environment-risk checks should go through `codex-task-gate` first.

## Rule

Do not immediately run expensive tests.

First recommend the most suitable test tier. Explain the recommended tier in detail, mention other tiers briefly, and ask for confirmation only when the test is costly, several tiers are reasonable, or the user asks for full testing.

## Test Tiers

- smoke test: cheapest sanity check; run one command or inspect one narrow path
- structure test: moderate check; validate file layout, imports, config, and obvious contracts
- full test: expensive check; run broad test suites, render/export workflows, or integration checks

## Output

Keep the plan natural and short, usually 250-400 Chinese characters with 2-4 brief paragraphs and light bullets only when useful.

Do not open by explaining that the request is a testing or verification scenario. Start with a natural judgment about whether full testing should run immediately and why.

Prefer openings like: "不建议一上来直接做完整测试。这个测试同时包含长文生成、Word 导出、PDF 渲染和页面 QA，一旦出问题，很难判断是内容、排版还是环境导致的。"

Include the three tiers as needed, using bilingual labels when helpful:

- 烟雾测试 smoke test
- 结构测试 structure test
- 完整测试 full test

Clearly recommend one tier, but do not force the user to choose. If the test is costly or the user explicitly asked for full testing, end with one short confirmation question about whether to proceed with the recommended plan.

## Recommended Level Detail Rule

When presenting a staged test plan, explain the recommended test level in detail. Mention the other levels in one sentence each, and do not explain the same level twice.

Example:

- 烟雾测试 smoke test：只验证能否生成最小输出。
- 结构测试 structure test：推荐。本轮生成 2-3 页样稿，覆盖标题、图表、公式、参考文献和导出链路，并检查关键排版问题。
- 完整测试 full test：等结构测试通过后，再做 5000+ 字或全量验收测试。

## Automatic Fallback Rule

During testing, if a route fails because a required local tool or environment is missing, do not stop immediately and do not retry the same route repeatedly.

Record that route as unavailable for this task, then automatically switch to the best available lower-cost fallback test.

Examples:

- DOCX/PDF rendering fails because LibreOffice, soffice, or a converter is missing: switch to DOCX structure QA, XML inspection, style checks, inline image checks, and table/formula layout checks.
- Android CLI build fails because Java or Gradle is missing: switch to static project structure and Gradle config inspection, then tell the user to sync/build in Android Studio.
- Git push fails because interactive authentication is unavailable: use an available GitHub connector or prepare zip/manual upload files.
- Visual rendering is unavailable: inspect file existence, dimensions, formats, embedded objects, and metadata where possible.

Ask the user only when no useful fallback exists, the fallback changes the requested deliverable, user choice is required, or critical input files are missing.

In the final summary, mention the failed route, why it was not retried, the fallback used, what was verified, and what remains unverified.
