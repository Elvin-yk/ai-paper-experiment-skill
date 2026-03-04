# AI Paper Experiment Skills

A small open-source skill collection for running paper experiments with Codex or other AI assistants.

## Included Skill

- `ai-paper-experiment-playbook`
  - Standard workflow for experiment planning, diagnosis, minimal patches, verification, and paper-ready summaries.
  - Location: `skills/ai-paper-experiment-playbook/`

## Install

Copy the skill folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -r skills/ai-paper-experiment-playbook ~/.codex/skills/
```

Then invoke it in chat with:

```text
$ai-paper-experiment-playbook
```

Or install directly from GitHub with Codex skill installer:

```text
$skill-installer install https://github.com/Elvin-yk/ai-paper-experiment-skill/tree/main/skills/ai-paper-experiment-playbook
```

## Trigger Examples

- "Use $ai-paper-experiment-playbook to debug this metric regression."
- "Use $ai-paper-experiment-playbook to plan a clean ablation study."
- "Use $ai-paper-experiment-playbook to turn these results into a paper-ready summary."

## Repository Layout

```text
skills/
  ai-paper-experiment-playbook/
    SKILL.md
    agents/openai.yaml
    references/
      experiment-record-template.md
      prompt-templates.md
```

## License

MIT License. See `LICENSE`.
