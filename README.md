# GPT-5.6 Prompt Optimizer

A lightweight Codex Agent Skill that rewrites prompts for GPT-5.6 using outcome-first instructions, explicit success criteria, bounded autonomy, focused tool routing, and observable stop conditions.

It preserves the user's intent and authorization while removing repeated rules, unnecessary process scaffolding, irrelevant tools, conflicting instructions, and requests for hidden chain-of-thought.

## Install

Clone the repository and copy the Skill into the user-level Codex Skills directory:

```bash
git clone https://github.com/highway-data/gpt56-prompt-optimizer.git
mkdir -p ~/.agents/skills
cp -R gpt56-prompt-optimizer/skills/optimize-gpt56-prompts ~/.agents/skills/
```

Codex normally detects new Skills automatically. Restart Codex if it does not appear.

## Use

Invoke it explicitly:

```text
$optimize-gpt56-prompts

Rewrite the following prompt for GPT-5.6 and return a copy-ready version:
[your prompt]
```

Codex can also invoke it implicitly when a request clearly asks to optimize, structure, compress, audit, or migrate a prompt. It does not intercept ordinary tasks.

By default, the Skill rewrites the prompt without executing the task inside it. Ask explicitly if both rewriting and execution are required.

## Design principles

- Preserve intent, facts, scope, language, authorization, and output requirements.
- Describe the desired outcome before prescribing a process.
- Keep true invariants and convert judgment calls into decision rules.
- Expose only relevant tools and prerequisite retrieval.
- Use observable success criteria, validation, and stop conditions.
- Keep simple prompts simple.
- Request auditable evidence and concise rationale, not hidden reasoning.

The guidance is based on OpenAI's [Prompting guidance for GPT-5.6](https://developers.openai.com/api/docs/guides/prompt-guidance-gpt-5p6) and [Codex Skills documentation](https://learn.chatgpt.com/docs/build-skills).

## Repository structure

```text
skills/optimize-gpt56-prompts/
├── SKILL.md
├── agents/openai.yaml
└── references/patterns.md
```

## License

MIT. This community project is not affiliated with or endorsed by OpenAI.
