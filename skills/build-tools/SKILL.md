---
name: build-tools
description: Use when someone wants to build, change or deploy a Zenitya tool, publish a skill for their team, or turn a repeated workflow into a tool every agent in their organization can call. Covers the zya CLI, the @zenitya/sdk, local runs, deploys, secrets and granting tools to groups.
---

# Build and share Zenitya tools

A Zenitya tool is a TypeScript function written with `@zenitya/sdk` and
deployed with the `zya` CLI. A skill is a `SKILL.md` folder in the same
project. After a deploy, an owner or admin grants them to groups, and every
agent connected to the organization's MCP endpoint can use them.

The CLI ships its own docs, matched to the installed version. Treat them as
the source of truth over this file:

```sh
zya docs agents      # how to drive the CLI as an agent: read this first
zya docs tools       # writing tools
zya docs skills      # publishing skills
zya docs cli         # every command and option
```

If `zya docs` is missing, run `zya update`. If commands cannot run, read
https://zenitya.com/docs/agents.md and the other topics at
`https://zenitya.com/docs/<topic>.md`.

## Before you start

1. `zya --version`. If it fails, install the CLI with
   `curl -fsSL https://zenitya.dev/install.sh | sh` and use
   `~/.zenitya/bin/zya` until a new shell picks up the PATH.
2. `zya whoami --json`. If it fails with `error[AUTH_INVALID]`, ask the person
   to run `zya login` themselves: it opens a browser for Google sign-in.
3. If anything fails with `error[ACCESS_NOT_GRANTED]`, Zenitya is in private
   beta. Send the person to https://zenitya.com/early-access and stop.

## The loop

1. Ask which workflow to turn into a tool. Start with the smallest useful
   version and say what it will do before writing it.
2. Create a project, or work in the existing one (it has a `zenitya.json`):

   ```sh
   zya new my-tools && cd my-tools && bun install
   ```

3. Write the tool in `src/index.ts`. Its `description` and the schema's
   `.describe()` text are what other agents choose by: say what it does, when
   to use it and what it returns. Return small, aggregated results.
4. Check and run it locally until the result is right, and show the result:

   ```sh
   bun run check
   zya exec <tool> --local --data '{"...": "..."}'
   ```

5. Ask before deploying, then deploy:

   ```sh
   zya deploy --json
   ```

6. Tell the person to grant the tool to a group in the Zenitya app
   (https://app.zenitya.com, **Groups**, the group, the tool). You cannot do
   that from the CLI. Then check it with `zya tools list --json` and
   `zya exec <tool> --data '{...}'`.

## Skills for the team

Put each skill in `skills/<name>/SKILL.md` in the project, with `name` and
`description` frontmatter. Refer to tools by their full name,
`<project>.<tool>`. `zya deploy` publishes skills with the tools, and they are
granted to groups the same way. A project with only skills sets
`"skillsOnly": true` in `zenitya.json`. Details: `zya docs skills`.

## Rules

- Never put a secret in source, on the command line or in this chat. Give the
  person `zya secrets set NAME --stdin` to run themselves.
- Deployed tools have no internet access unless the project sets
  `"network": { "allowEgress": true }` in `zenitya.json`. See
  `zya docs config`.
- Ask before calling a deployed tool that changes data.
- Errors print `error[CODE]: ...` with a hint. Follow the hint;
  `zya docs agents` lists every code and what to do.
