---
name: replit-deployment
description: Prepares a Replit app for deployment, covering deployment type choice, build and run commands, health checks, port binding, and dev versus production differences. Use when the user wants to publish, deploy, or fix a deployment that builds in the workspace but fails or behaves differently when deployed.
compatibility: Designed for Replit Agent and Replit workspaces.
metadata:
  version: "1.0"
---

# Replit Deployment

## Scope

Use this skill before publishing a Replit app and when a deployed app behaves differently from the workspace. Workspace config is covered in `replit-config`, and secrets in `replit-secrets`.

## Choose the deployment type

Confirm the options currently offered in the Replit Deployments UI, since names and availability change. Match them to the workload:

- **Static site:** no server code, only built assets.
- **Autoscale:** stateless web apps and APIs with variable traffic.
- **Reserved VM:** long-running processes, background workers, or anything holding state in memory or connections open.
- **Scheduled:** jobs that run on a timetable and exit.

Ask the user if the choice isn't clear from the code. Don't guess for a paid option.

## Pre-deploy checks

1. **Separate build from run.** Dependencies install and assets build in the build command. The run command only starts the server.
2. **Production start command.** Use a production server (for example gunicorn, `node dist/server.js`), not a dev server or file watcher.
3. **Port.** Bind to `0.0.0.0` and read `PORT` from the environment.
4. **Local disk is not durable.** Don't store uploads, SQLite databases or sessions on the deployment's filesystem. Use the managed database or object storage.
5. **Secrets.** Confirm every secret the app reads exists for the deployment, not only the workspace.
6. **Health.** The root path or a `/health` route should return 200 quickly, without waiting on slow dependencies.
7. **Logs.** Write to stdout and stderr so the deployment logs show them.

## When deployed differs from the workspace

Check in this order: missing secret, missing build step, dev dependency needed at runtime, hardcoded `localhost` URL, port binding, filesystem writes, and the database pointing at the wrong environment.

## Output

State the deployment type chosen and why, the build and run commands, and each check as pass, fail or not verified.
