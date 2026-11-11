# Zenitya plugin

[Zenitya](https://zenitya.com) keeps your team's custom tools and Agent Skills
in one place and serves them to every agent through one MCP connection. This
plugin adds that connection to your agent, plus two skills:

- **setup** checks the connection and sign-in and shows the tools and skills
  your groups give you.
- **build-tools** teaches your agent to build, test and deploy new tools and
  skills with the `zya` CLI, so one person builds a workflow and the whole team
  has it.

The plugin follows [Agent Plugins 1.0.0](https://agent-plugins.org) and also
ships a Claude Code manifest.

> Zenitya is in private beta. Signing in needs an invitation from your team or
> [early access](https://zenitya.com/early-access).

## Install

### Claude Code

```text
/plugin install zenitya --marketplace Zenitya/zenitya-plugin
```

Then run `/mcp`, choose **zenitya** and sign in with Google.

### Codex and the ChatGPT desktop app

```sh
codex plugin marketplace add Zenitya/zenitya-plugin
```

Then open `/plugins` in Codex, or **Plugins** in the ChatGPT desktop app,
install **Zenitya** and sign in when asked.

### Any other agent

Add the MCP server directly. It is a remote server over streamable HTTP with
OAuth sign-in:

```text
https://api.zenitya.com/mcp
```

Setup steps for each client are in the
[docs](https://zenitya.com/docs/mcp). Clients that support Agent Plugins can
also install this repository as a plugin folder.

## What's inside

```text
plugin.json                  Agent Plugins manifest
mcp.json                     the Zenitya MCP server
skills/setup/                onboarding skill
skills/build-tools/          building and deploying tools and skills
.claude-plugin/              Claude Code manifest and marketplace
.agents/plugins/             Codex marketplace
server.json                  the official MCP Registry entry
```

## Links

- [Website](https://zenitya.com)
- [Docs](https://zenitya.com/docs)
- [@zenitya/sdk on npm](https://www.npmjs.com/package/@zenitya/sdk)
- [Privacy](https://zenitya.com/privacy) and [terms](https://zenitya.com/terms)

## License

MIT
