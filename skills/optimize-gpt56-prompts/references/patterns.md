# GPT-5.6 prompt patterns

Read only the pattern that matches the supplied prompt. Preserve the user's actual values and omit irrelevant fields.

## Compact task

```text
Goal: [result]
Context: [only facts that change the result]
Output: [usable format and audience]
Boundary: [the one or two constraints that prevent a real problem]
```

Use for summaries, rewrites, comparisons, explanations, and other short tasks.

## Local implementation

```text
Goal: [requested local change]

Success criteria:
- [observable behavior]
- [required artifact]

Authorization and constraints:
- Limit changes to [scope].
- Preserve [existing behavior or user work].
- Do not commit, push, deploy, or change production unless explicitly requested.

Validation:
- Run the smallest relevant checks for the changed behavior.
- Distinguish static checks, isolated tests, real execution, and business confirmation.
- If a check cannot run, state why and give the next-best verification.

Output: Lead with the result, then changed files, validation, and remaining risk.

Stop rules: Finish after the requested behavior and relevant checks pass. Do not add speculative features or unrelated cleanup.
```

## Read-only diagnosis or review

```text
Goal: Determine [question] from the current repository or artifacts.

Evidence boundary:
- Confirm the real repo, branch or fixed point, entrypoint, and current outputs.
- Bind conclusions to files, lines, logs, timestamps, or results.
- Separate confirmed facts, inference, and unverified claims.

Authorization: Read and report only. Do not modify files or external state.

Output: Findings first, ordered by impact, followed by checked scope, evidence, uncovered validation, and verdict.

Stop rules: Stop when the core question has enough evidence. If required evidence is missing, name the smallest missing fact instead of guessing.
```

## Source-grounded research

```text
Goal: Answer [research question] for [decision or audience].

Source rules:
- Use [required source types or named artifacts].
- Support material current claims with retrieved sources.
- Attach citations to the claims they support.
- Label inference and source conflicts explicitly.

Retrieval budget:
- Start with one focused retrieval pass.
- Retrieve again only for a missing required fact, requested comparison or exhaustiveness, a named artifact, or an unsupported material claim.
- Do not retrieve again only to improve phrasing or add optional examples.

Output: [decision-ready format].

Stop rules: Narrow the conclusion or report missing evidence instead of converting absence of evidence into a factual no.
```

## Long-running or tool-heavy workflow

```text
Goal: [end-to-end outcome]

Current layer: [research | design | implementation | review | external coordination]

Progress updates:
- Before the first tool call, state the first phase in one or two sentences.
- Update only when a major phase starts or a finding changes the plan.
- Report outcomes and the next step, not routine commands.

Tool rules:
- Resolve prerequisites before action.
- Parallelize independent reads; serialize dependencies and writes.
- After each result, decide whether the core request can now be completed.
- Try at most two meaningful fallbacks for partial or suspicious results.

State and stopping:
- Compact after milestones, not every turn.
- Reuse prior reasoning only while objectives and assumptions remain stable.
- Stop when the completion bar is met; otherwise name the blocker or smallest missing input.
```

## Migration check

When adapting an existing GPT-5.5 or GPT-5.4 prompt to GPT-5.6:

1. Preserve the current model behavior and reasoning effort as the evaluation baseline.
2. Change the model before rewriting the prompt.
3. Compare representative tasks.
4. Remove one group of obsolete scaffolding, repeated rules, examples, or tools at a time.
5. Add only a targeted instruction for an observed regression.
6. Compare quality, completeness, evidence, tokens, latency, cost, calls, and retries.
7. Count efficiency as an improvement only when the result still passes the existing acceptance criteria.

## Final lint

- The outcome is explicit.
- Facts and authorization are preserved.
- Success and stopping conditions are observable.
- True invariants are distinct from judgment rules.
- Evidence and tool prerequisites are present only when needed.
- No rule is repeated in different wording.
- No unavailable tool, source, permission, or API parameter was invented.
- No hidden chain-of-thought or private reasoning was requested; use auditable evidence and concise rationale instead.
- A simple request stayed simple.
