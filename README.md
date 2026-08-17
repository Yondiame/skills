# User Intuition Skills

Pre-built [Claude Code](https://claude.com/claude-code) skills for running customer research with [User Intuition](https://www.userintuition.ai) — create interview studies, design screeners, field panel recruits, and turn transcripts into stakeholder-ready findings.

Where the [User Intuition MCP server](https://docs.userintuition.ai/mcp-server/overview) gives your agent the *tools*, these skills give it the *play*: the workflow, the guardrails, and the order of operations that make research runs reproducible.

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add user-intuition/skills
/plugin install user-intuition-research@user-intuition
```

### Any agent (raw files)

Each skill is a standalone Markdown file under `plugins/user-intuition-research/skills/<name>/SKILL.md`. Claude Code discovers skills as one directory per skill — copy any of them to `~/.claude/skills/<name>/SKILL.md` — or tell your agent:

> Fetch https://docs.userintuition.ai/skills/library.md and install each skill as `~/.claude/skills/<name>/SKILL.md` — one directory per skill

## Prerequisites

The skills drive the User Intuition MCP server — connect it first ([quickstart](https://docs.userintuition.ai/mcp-server/quickstart)):

```bash
claude mcp add userintuition -- npx -y @userintuition-ai/mcp
```

with `USERINTUITION_API_KEY` set (get a key from your [dashboard](https://app.userintuition.ai)).

## The skills

| Skill | Outcome |
|-------|---------|
| `create-study-from-brief` | Turn a research brief into a launch-ready interview study |
| `design-screeners` | Recruit exactly the right respondents — panel and custom screeners, done safely |
| `field-a-panel` | Recruit N respondents from the panel, with cost approved before any spend |
| `invite-your-own-participants` | Interview your own customers — invites, share links, and rewards |
| `run-a-concept-test` | Put a concept, prototype, or landing page in front of participants |
| `monitor-fielding` | Daily digest of every fielding study — progress, quality, stalls |
| `analyze-completed-study` | From transcripts to stakeholder-ready findings, with real quotes only |
| `curate-interview-quality` | Keep low-quality interviews out of your analysis — reversibly |

Every tool name and argument is verified against the published `@userintuition-ai/mcp` package. Check any tool yourself:

```bash
npx -y @userintuition-ai/mcp describe create_study
```

## Docs

- [Skills overview](https://docs.userintuition.ai/skills/overview)
- [Skills library](https://docs.userintuition.ai/skills/library) (browsable version of these files)
- [MCP server reference](https://docs.userintuition.ai/mcp-server/overview)

## License

MIT
