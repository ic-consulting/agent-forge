---
name: replit-config
description: Configures a Replit project through the .replit file and replit.nix, covering run commands, language modules, system packages, and port mappings. Use when a Replit app won't start, a package or runtime is missing, the preview shows nothing, or the user asks to change how the project runs.
compatibility: Designed for Replit Agent and Replit workspaces.
metadata:
  version: "1.0"
---

# Replit Config

## Scope

Use this skill when changing how a Replit project is built and run. Deployment settings are covered in `replit-deployment`, and secrets in `replit-secrets`.

## Steps

1. Read `.replit` and `replit.nix` (if present) before changing anything. Hidden files may not show in the file tree.
2. Identify the problem class:
   - **Won't start:** check the `run` command and the language `modules`.
   - **Missing system library or tool:** add it to `replit.nix` under `deps`, not with `apt` or a global install, which don't persist.
   - **Preview is blank or the port isn't reachable:** check the server binds to `0.0.0.0` (not `localhost` or `127.0.0.1`) and that a `[[ports]]` entry maps the local port.
3. Make the smallest edit that fixes it. Don't rewrite the whole file.
4. Restart the Repl and confirm the app starts and the preview loads. Report what you ran, not what you expect.

## Rules of thumb

- Keep `.replit` and `replit.nix` in version control. They are the project's environment.
- Use one `run` command that starts the app. Put multi-step startup in a script and call that.
- Pin runtime versions through `modules` instead of relying on the default.
- Read the port from the `PORT` environment variable, with a fallback for local use.
- Don't hardcode absolute paths from the workspace. They differ in deployments.

## Output

Show the exact diff to `.replit` or `replit.nix`, the reason, and how you verified it. If you couldn't verify it (for example, no shell access), say so.
