---
name: replit-secrets
description: Handles secrets and environment variables in a Replit project, including how to store, read, and rotate them and how to find leaked credentials. Use when the user adds an API key, sees a missing environment variable, or when code contains hardcoded credentials or a committed .env file.
compatibility: Designed for Replit Agent and Replit workspaces.
metadata:
  version: "1.0"
---

# Replit Secrets

## Scope

Use this skill whenever a Replit project needs an API key, token, password or connection string. Pair it with `security-assessment` for a full sweep.

## Rules

1. **Store credentials in Replit Secrets.** They are exposed to the app as environment variables. Never write them into source, `.replit`, `replit.nix`, README files or chat.
2. **Read them from the environment.** For example `os.environ["KEY"]` or `process.env.KEY`. Fail at startup with a clear message naming the missing variable (never its value).
3. **Don't commit `.env` files.** Add `.env*` to `.gitignore` and check it isn't already tracked.
4. **Separate non-secret config.** Hostnames, feature flags and log levels can live in code or `[env]` in `.replit`. Anything that grants access is a secret.
5. **Don't print secrets.** Keep them out of logs, error messages and client-side bundles. Variables prefixed for the browser (such as `VITE_` or `NEXT_PUBLIC_`) are public.
6. **Deployments need their own copy.** Confirm the secret is available to the deployment as well as the workspace.

## If a secret may have leaked

1. Treat it as compromised. Revoke or rotate it at the provider first.
2. Update the value in Secrets.
3. Remove it from the code. Rewriting git history doesn't un-leak it, so rotation is the real fix.
4. Search for other copies: `git log -p -S'<prefix>'` and the bundled scanner in `security-assessment`.

## Output

List each secret the app needs by name only (never the value), where it is read, and whether it is set for the workspace and the deployment.
