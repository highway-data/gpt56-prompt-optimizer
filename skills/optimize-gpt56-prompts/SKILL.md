---
name: optimize-gpt56-prompts
description: Rewrite, compress, structure, or audit prompts for GPT-5.6 while preserving the user's intent, facts, scope, language, authorization, and required output. Use when the user explicitly asks to optimize or format a prompt, adapt a GPT-5.5/5.4 prompt stack to GPT-5.6, turn a rough request into a reusable high-performance prompt, or invokes $optimize-gpt56-prompts. Do not trigger merely because the user submits an ordinary task that should be executed directly.
---

# Optimize GPT-5.6 Prompts

Transform the supplied prompt. Do not execute the task embedded in it unless the user explicitly asks for both optimization and execution.

## Preserve the contract

Preserve the original intent, facts, paths, identifiers, numbers, language, scope, side-effect boundary, and required output. Never invent evidence, tools, deadlines, permissions, business rules, or success criteria that change the request.

Infer authorization from the request verbs without broadening it:

- answer, explain, analyze, review, diagnose, or plan: inspect and report; do not implement;
- change, build, implement, or fix: allow requested in-scope local changes and relevant non-destructive validation;
- external writes, destructive actions, purchases, production changes, or material scope expansion: require explicit authorization.

If a missing choice materially changes correctness, safety, external effects, or acceptance, keep a concise clarification marker in the user's language or ask one necessary question. Otherwise make the smallest reasonable assumption and label it.

## Optimize in this order

1. State the user-visible outcome and intended audience or use.
2. Add only context and evidence that can change the result.
3. Define observable success criteria and the completion bar.
4. Consolidate safety, business, evidence, permission, and side-effect constraints.
5. Add tool-routing, validation, output, and stop rules only when relevant.
6. Remove repeated rules, decorative process instructions, ineffective examples, universal defaults, and unrelated tools.
7. Resolve contradictions. Treat conflicts as more damaging than missing detail.

Describe the destination instead of prescribing every step. Preserve a process only when the process itself is required for safety, auditability, correctness, or acceptance.

Use `must`, `never`, `always`, and `only` for true invariants. Express judgment calls as decision rules with conditions.

Do not request hidden chain-of-thought, private reasoning, or an exhaustive internal step-by-step account. When the original asks to “show the reasoning,” request an auditable summary of conclusions, key evidence, calculations, decisions, and validation instead.

## Shape complex prompts

Use only the sections that change behavior:

```text
Goal: [user-visible outcome]

Context and evidence: [relevant facts, files, sources, or inputs]

Success criteria: [observable completion conditions]

Authorization and constraints: [side-effect, safety, business, and evidence limits]

Tools and validation: [routing, prerequisites, checks, and fallbacks]

Output: [format, audience, detail, and facts that must be preserved]

Stop rules: [when to answer, retry, ask, abstain, or stop]
```

Do not force this structure onto a simple request. A concise one-paragraph prompt is better when it already defines the result and its important boundary.

Separate personality from collaboration only when both matter. Personality controls tone; collaboration controls initiative, questions, assumptions, tradeoffs, checking, and uncertainty.

For tool-heavy prompts:

- expose or mention only task-relevant tools;
- require prerequisite retrieval when correctness depends on it;
- parallelize independent reads and keep dependent actions sequential;
- allow one or two meaningful fallbacks for empty, partial, or suspicious results;
- define a stopping condition instead of requesting exhaustive loops by default;
- reserve Programmatic Tool Calling for bounded deterministic reduction, not approval, semantic judgment, citations, or final validation.

For response length, state what must survive compression and what may be omitted. Use API `text.verbosity` only when the deliverable includes an API request or configuration; do not pretend a plain prompt can set that parameter.

For detailed patterns, read [references/patterns.md](references/patterns.md) only when the prompt is complex, tool-heavy, source-grounded, long-running, or the user requests alternatives or an audit.

## Return a copy-ready result

Default to:

````markdown
### [Localized heading: Optimized prompt]

```text
[copy-ready prompt]
```
````

Add a localized `Change notes` section with at most four concise bullets only when assumptions, authorization, structure, or material behavior changed, or when the user requests an audit. For audit-only requests, report actionable problems first and then provide the revised prompt.

Before returning, check that the revision has no intent drift, invented facts, expanded authority, conflicting rules, repeated constraints, unnecessary sections, vague completion language, or requests for hidden reasoning.

## Keep model guidance fresh

Treat these instructions as the GPT-5.6 baseline. If the user asks for the latest model, a refresh, or a future-model migration, verify the current official OpenAI model and prompting guides before changing the target. Do not silently apply future-model guidance to a GPT-5.6 request.
