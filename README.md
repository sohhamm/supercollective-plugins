<p align="center"><img src="assets/supercollective.png" width="96" height="96" alt="SuperCollective logo"></p>

# SuperCollective plugins

Agent plugins and MCP servers for [SuperCollective](https://supercollective.studio) products. Each plugin connects your agent to a product's hosted MCP server and adds a skill that teaches the agent the product's rules.

| Plugin | What it does | Server |
| --- | --- | --- |
| [TesterSwap](plugins/testerswap) | Manage your app tests and credits; real people do the testing | `https://api.testerswap.com/mcp` (OAuth) |

## Install

### Cursor

Install from the Cursor Marketplace, or add a plugin's server to `~/.cursor/mcp.json` as shown in its README.

### Claude Code

```
/plugin marketplace add sohhamm/supercollective-plugins
/plugin install testerswap@supercollective
```

### Other MCP clients

Every plugin's README lists its server URL and authentication. Add it as a remote MCP server in Claude, ChatGPT or any client that supports Streamable HTTP.

## Layout

```
.cursor-plugin/marketplace.json   Cursor catalog
.claude-plugin/marketplace.json   Claude Code catalog
plugins/<name>/
  .cursor-plugin/plugin.json      Cursor manifest
  .claude-plugin/plugin.json      Claude Code manifest
  mcp.json                        Cursor server config
  .mcp.json                       Claude Code server config
  server.json                     Official MCP registry entry
  skills/<name>/SKILL.md          Agent instructions
  assets/logo.png                 512x512 logo on a background plate
  README.md
```

A new plugin needs its folder and an entry in both catalogs. Validate with `claude plugin validate plugins/<name>` before opening a pull request.

## Support

[support@supercollective.studio](mailto:support@supercollective.studio). Each plugin's README links its product's privacy policy and terms.

## License

MIT. Each product's hosted service is governed by its own terms.
