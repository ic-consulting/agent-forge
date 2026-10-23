# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Two things in one repo:

1. **`agent-install`**, a stdlib-only Go CLI (module `claudeinstaller`, Go 1.25, no dependencies). It is a single `package main` in `main.go`, with tests in the sibling `*_test.go` files.
2. **The content it distributes**, under `configs/`: `agents/*.md`, `rules/*.md`, and `skills/<name>/{SKILL.md,checklist.md,...}`.

`configs/` is the source of truth. `.claude/` is gitignored and holds a local installed copy. Edit `configs/`, never `.claude/`, or the change won't be committed.

## Commands

```bash
go build -o bin/agent-install .   # build (bin/ is gitignored)
go test ./...                     # all tests
go test -run TestName ./...       # a single test
go vet ./...
./build.sh                        # cross-compile all OS/arch targets + SHA256SUMS into ./bin
```

CI (`.github/workflows/build.yml`) runs vet, test, `staticcheck@v0.7.0` (pinned to the newest release that supports the Go version in `go.mod`; bump it together with `go.mod`), then `build.sh`. Pushing a `v*` tag publishes a release.

## Architecture

`main()` requires exactly one action flag (`countActions`). The actions fall into two groups:

- **Remote actions** (`-contents`, `-dryrun`, `-install`): `downloadConfig` fetches the GitHub source zip for `-repo`@`-version`, and `extractConfig` keeps only the `configs/{agents,skills,rules}` files in an in-memory `memFS`. `plan` compares each file against `<target>/...` and marks it NEW, SAME or OVERWRITE. `runInstall` backs overwritten files up as `.bak`. `-dryrun` is the same path with writes disabled.
- **Local actions** (`-agent`, `-skill`, `-review`, `-serve`): these read from the installed `-target` directory (default `~/.claude`) and never touch the network. `-review <file>` picks a reviewer agent via `reviewerFor`, which maps the extension or filename to an agent (Dockerfile, compose and CI YAML go to `devops-reviewer`, and anything unknown goes to `code-reviewer`). It then calls `runAgent`. `-serve` exposes the same data over HTTP, built by `newServeMux`.

Security-relevant details to preserve:
- Agent and skill names must match `validName` before they touch the filesystem. The HTTP server serves only the files listed in `skillFiles`.
- `-serve` binds to `127.0.0.1:8081` by default.
- `githubURL` is a package var so tests can point it at an `httptest` server.

## Content conventions

- Agents (`configs/agents/*.md`) have YAML frontmatter (`name`, `description`, `tools`, `model`, `permissionMode`). Their bodies tell the agent to read `~/.claude/rules/<x>.md` first, so rule file names are referenced by agents. Renaming one means updating the agents that reference it.
- The `*-dev` agents pair with `*-reviewer` agents, and the `-dev` agents implement against the matching `rules/` file.
- New reviewers also need an entry in `reviewersByExt` in `main.go` (plus a test in `review_test.go`) if they should be auto-selected by `-review`.
- `INTEGRATION_GUIDE.md` documents the CLI and HTTP API, and `README.md` documents installation and the flag reference. Update both when changing flags or endpoints.

## Git workflow

Per `configs/rules/git-workflow.md`: never commit to `main`. Branch as `type/short-description` (`feat/`, `fix/`, `chore/`, `docs/`, `refactor/`). Use short imperative commit subjects of 72 characters or fewer, one logical change per commit. Don't force-push shared branches. CI must pass before merge.
