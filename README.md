# Canon Plugin for Claude Code

Spec-driven development, automated. Verify code against specs, track coverage, and maintain living documentation — all from within Claude Code.

**[Website](https://canonhq.co)** · **[Documentation](https://canonhq.co/docs)** · **[Getting Started](https://canonhq.co/docs/getting-started/)**

## Installation

```
/plugin marketplace add canonhq/canon-claude-plugin
/plugin install canon
```

Requires [Claude Code](https://claude.com/claude-code) and Python 3.12+ (for the MCP server, installed automatically via `uvx`).

## Skills

| Skill | Description |
|-------|-------------|
| `/canon:context` | Load relevant spec context for your current task |
| `/canon:task` | Pick up a spec task, implement acceptance criteria, mark done |
| `/canon:verify` | Verify code against spec acceptance criteria |
| `/canon:new` | Create a new spec from template |
| `/canon:plan` | Spec-driven implementation planning |
| `/canon:review` | Detect drift between code and documentation |
| `/canon:status` | Spec coverage dashboard |
| `/canon:update` | Sync spec statuses from code evidence |
| `/canon:audit` | Full spec maintenance — status sync, drift detection, coverage |

## How It Works

Canon treats documentation as living programs. You write structured specs with acceptance criteria, and Canon's agents keep everything in sync as you build.

1. **Stay in context** — automatically surfaces relevant specs when you're working
2. **Verify implementation** — checks your code against spec acceptance criteria and marks them realized
3. **Track progress** — coverage dashboard shows what's done and what's left
4. **Keep docs current** — detects drift between code and documentation

Learn more about the concepts behind Canon: [Living Specs](https://canonhq.co/docs/concepts/living-specs/), [Spec Coverage](https://canonhq.co/docs/concepts/spec-coverage/), [Delta Tracking](https://canonhq.co/docs/concepts/delta-tracking/).

## MCP Server

The plugin includes a Canon [MCP server](https://canonhq.co/docs/reference/mcp-tools/) that gives Claude structured access to your specs:

- **search** — hybrid search across specs
- **get_spec** / **get_section** — read parsed spec data
- **create_spec** — create new specs from templates
- **update_section_status** — update section statuses
- **add_realization** — link code evidence to acceptance criteria
- **sync_spec_status** — bulk status updates in one commit

All skills work without MCP using local file operations. MCP adds semantic search, write-back to GitHub, and org-wide coverage metrics.

## Spec Format

Specs live in `docs/specs/*.md` as structured markdown with YAML frontmatter. See the [Spec Format Reference](https://canonhq.co/docs/reference/spec-format/) and [Writing Specs Guide](https://canonhq.co/docs/guides/writing-specs/) for full details.

```yaml
---
title: "Feature Name"
type: spec
status: draft
owner: "name"
team: "team-name"
tags: [auth, api]
---
```

Sections use numbered headings with acceptance criteria:

```markdown
## 1. Login Flow

<!-- canon:system:1 status:in_progress -->

### Acceptance Criteria

- [x] Email validation
- [ ] Rate limiting
<!-- canon:realized-in:PR#42 file:src/auth.py:10-25 -->
```

## Configuration

The plugin reads `CANON.yaml` from your repo root. See the [Configuration Reference](https://canonhq.co/docs/reference/canon-yaml/) for all options.

```yaml
specs:
  doc_paths:
    - "docs/specs/*.md"
  require_review: true

agents:
  pr_analysis: true
  doc_updates: true
```

Run `canon setup` to initialize a new repo, or follow the [Quickstart Guide](https://canonhq.co/docs/getting-started/quickstart/).

## Resources

- [Documentation](https://canonhq.co/docs) — full reference, guides, and concepts
- [CLI Reference](https://canonhq.co/docs/reference/cli/) — `canon` CLI commands
- [GitHub App Setup](https://canonhq.co/docs/guides/github-app-setup/) — automated PR analysis and doc updates
- [Self-Hosting Guide](https://canonhq.co/docs/guides/self-hosting/) — deploy Canon on your own infrastructure

## License

MIT
