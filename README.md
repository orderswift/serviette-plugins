# Serviette plugins

Plugins that let an AI assistant order food to collect from independent restaurants on [Serviette](https://withserviette.com), using its MCP server at `https://agent.withserviette.com/agent/mcp`.

| Folder     | For                              | What it is                                                                                  |
| ---------- | -------------------------------- | ------------------------------------------------------------------------------------------- |
| `claude/`  | Claude (claude.ai, Cowork, Code) | A Claude plugin: manifest, `.mcp.json`, the `order-takeaway` skill                          |
| `chatgpt/` | ChatGPT (and Codex)              | An OpenAI plugin package: `plugin.json`, `mcp.json`, the skill, the logo, review test cases |

The repository root is also a Claude marketplace (`.claude-plugin/marketplace.json`) that lists the Claude plugin.

Neither plugin holds any code or credentials: both only point the assistant at the MCP server and tell it how to take an order. Sign-in for saved orders is handled by the server's OAuth flow when a tool needs it.

See `SUBMITTING.md` for what is left to do before each is submitted.
