# Replit skills

Skills for Replit Agent, following the [Agent Skills specification](https://agentskills.io/specification). Each folder under `skills/` is one skill with a `SKILL.md` and optional `references/` and `scripts/`.

| Skill | Purpose |
|-------|---------|
| `replit-config` | `.replit` and `replit.nix`, run commands, ports |
| `replit-deployment` | Choosing a deployment type and pre-deploy checks |
| `replit-secrets` | Secrets and environment variables |
| `api-design-patterns` | Pagination, versioning, errors, webhooks |
| `database-optimization` | PostgreSQL query and index analysis |
| `frontend-accessibility` | WCAG 2.2 AA guidance |
| `performance-assessment` | CPU, memory, I/O and latency |
| `security-assessment` | Security sweep with a secrets scanner |
| `testing-patterns` | Test strategy by language |
| `ui-design` | Intentional, non-generic UI: type, colour, layout, states, copy |

`ui-design` is original to this folder. `api-design-patterns`, `database-optimization`, `frontend-accessibility`, `performance-assessment`, `security-assessment` and `testing-patterns` are adapted from `configs/skills/`: the checklist moved to `references/`, and Claude Code-specific paths and agent references were removed. Keep the two copies in sync by hand.

## Connecting Replit

Connect the Replit project to this repository with the GitHub integration, then point Replit at `configs/replit/skills`. Check Replit's current documentation for where it looks for skills, since this may require copying or symlinking the folder to the path it expects.

## Validating

```bash
skills-ref validate configs/replit/skills/<skill-name>
```
