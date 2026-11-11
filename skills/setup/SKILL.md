---
name: setup
description: Use right after the Zenitya plugin is installed, or when someone asks what Zenitya is, whether their Zenitya connection works, or which team tools and skills they have. Checks the MCP connection and sign-in, handles the private beta, and summarises what the person's groups give them.
---

# Set up Zenitya

Zenitya serves an organization's custom tools and Agent Skills to every agent
through one MCP server, `zenitya`, at `https://api.zenitya.com/mcp`. What a
person sees depends on the groups they belong to in their organization.

## 1. Check the connection

Call `list_skills` on the `zenitya` server.

- **It answers:** the connection works. Go to step 3.
- **The server asks for sign-in, or the client shows it as needing
  authentication:** go to step 2.
- **It fails with `access_not_granted`, or sign-in ends on a waitlist page or
  a page saying the person needs to join an organization:** Zenitya is in
  private beta. Tell the person that an invitation from their team admits
  them, or that they can request access at https://zenitya.com/early-access.
  Stop here.

## 2. Sign in

Sign-in happens in the browser with Google, and only the person can complete
it. Tell them how for their client:

- **Claude Code:** run `/mcp`, choose **zenitya** and sign in.
- **Codex CLI:** run `codex mcp login zenitya`.
- **ChatGPT, Cursor, VS Code and others:** open the client's MCP or plugin
  settings and select **Authenticate** or **Connect** next to Zenitya.

They choose their organization and approve access. Then go back to step 1.

## 3. Show what they have

1. List the tools on the `zenitya` server. Tool names are
   `<project>_<tool>` or `<project>.<tool>`, depending on the client: group
   them by project.
2. From the `list_skills` result, name each skill with its description in a
   few words.
3. Summarise both in a short list, and suggest one or two questions the person
   could ask that use them.

If there are no tools and no skills, the person's organization has not granted
any to their groups yet. An owner or admin grants them in the Zenitya app at
https://app.zenitya.com under **Groups**.

## Next

If the person wants to build a tool or publish a skill for their team, use
the `build-tools` skill.

At the start of every later task, call `list_skills` and load the skills that
match it with `load_skill`. They describe how this organization works.
