# 🧠 Learning Lesson: Getting Started with MCP

- **Before diving into the practical setup, make sure to read this essential [article](https://medium.com/qdrddr/0c02f3915867) that covers the basics of MCP.** The concepts explained in the article will help you understand the practical steps in this guide.

## 🚀 What You'll Learn

By the end of this lesson, you'll be able to:

- Understand what MCP is and why it's important
- Connect MCP Client to local and cloud-based MCP Servers
- Understand transport protocols and proxies
- Be aware of MCP's limitations
- Will take approximately 15 minutes

---

## 📌 What is MCP?

**Model Context Protocol (MCP)** allows Large Language Models (LLMs) to interact with your real-world data, applications, and tools by adding **context** they wouldn't otherwise know (e.g. your calendar, files, or CRM).

MCP bridges LLMs and your environment through:

- **MCP Servers** – Expose tools, resources, or data
- **MCP Clients** – Interface for the LLM to talk to servers
- **MCP Proxy** – Translates between server "languages": STDIO, SSE, streamable-HTTP

> 💡 Think of MCP as giving ChatGPT or Claude access to your apps and tools in a controlled, programmable way.

---

## 🖥️ MCP Client

- **MCP Client** Is a software that can connect to MCP Servers to get their available tools and provide those tools to your LLM. It supports:

- Consume in your custom code such as Python with [FastMCP module](https://github.com/modelcontextprotocol/python-sdk)
- Or with User-Interface-based applications such as: [Cursor](https://www.cursor.com/), [Windsurf](https://windsurf.com/), [VS Code GitHub Copilot](https://github.com/features/copilot), VS Code extentions: [RooCode](https://marketplace.visualstudio.com/items?itemName=RooVeterinaryInc.roo-cline), [Cline](https://cline.bot/), [Continue](https://marketplace.visualstudio.com/items?itemName=Continue.continue).

---

## ⚙️ MCP Transport
Each MCP Server may speak with one of a couple of these "languages" (MCP Transport Protocols). 

- STDIO - typically with locally installed MCP Servers 
- SSE - sometimes with locally installed MCP Servers, more often with cloud-based MCP Servers
- Streamable-HTTP - sometimes with locally installed MCP Servers, more often with cloud-based MCP Servers

### MCP Proxy
Same goes to MCP Clients, which may not speak MCP Server's language, that's where you'll need MCP Proxy to translate:
- **MCP-Remote** – Simple Streamable-HTTP & SSE → STDIO proxy with auth. Your go-to first choice since most MCP Clients support STDIO.
- **MCP-Proxy** - For SSE ⇄ STDIO or SSE ⇄ StreamableHttp
- **SuperGateway** - Converts between STDIO and HHTP-based transports (SSE, StreamableHttp, WebSockets)

### 1. Locally running MCP Servers

To run MCP Servers locally you'll need these tools installed:
- Locally with [`npm`/`npx`](https://github.com/npm/cli), [`uv`/`uvx`/`pip`](https://docs.astral.sh/uv/getting-started/installation/), [`bun/bunx`](https://bun.sh/docs/installation), [`node`](https://nodejs.org/en/download). Note when you install `uv` it also has `uvx`, and `npm` has build-in `npx` and the same with `bun`/`bunx`. Most of the commands starting with `pip` can be replaced with `uv pip` or `uvx`. Most of the time installed like this MCP Servers support STDIO-only but may support SSE or even Streamable-HTTP transports.
- In containers [Docker](https://www.docker.com/products/docker-desktop/) ([docs](https://docs.docker.com/get-started/get-docker/)) / [Podman](https://podman-desktop.io/downloads) - may support one or a few transport protocols.
- Via MCP Toolkit (Docker Desktop extension) - STDIO-only.

To prepare for this please go ahead and install Docker Desktop, `npm`, `uv` and `bun` on your local computer using the links above.

#### 1.1 Docker Desktop
- Install [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Open the app, in the right panel find "Extensions", Press "Manage", then select "Browse" tab, search "MCP Toolkit", Press "Install"

#### 1.2 **How uvx & npx work**
If for example you need to use `mcp-server-time` MCP Server locally, with uvx you don't need to install it! That's the whole point of using uvx (just like npx).

**`uvx mcp-server-time` will:**

- Automatically download and install mcp-server-time in a temporary, isolated environment
- Run it immediately
- Clean up after execution (unless you specify otherwise)
- This is similar to how `npx @mcp/filesystem` works - it downloads and runs the package without requiring a separate installation step, you just need `npm` installed.
- Same goes for `bunx @sylphlab/filesystem-mcp` just install `bun`

### 2. Remotely running MCP Servers
From online services with native MCP support (e.g. GitHub, DeepWiki, [Cloudflare](https://developers.cloudflare.com/agents/model-context-protocol/mcp-servers-for-cloudflare/)).
Some may support SSE only or streamable-HTTP only or both:
- **SSE:** example https://mcp.deepwiki.com/sse (note /sse at the end indicating SSE protocol)
- **Streamable-HTTP:** example https://mcp.context7.com/mcp (note /mcp at the end indicating StreamableHttp)
- **Streamable-HTTP with Auth:** example https://api.githubcopilot.com/mcp/ [read more](https://github.com/github/github-mcp-server)

In some cases Auth is not needed, like for example https://mcp.deepwiki.com/ that works as a public source of documentation that our MCP Clients only reads from the website while others require some form of Authentication using login & password, API keys. And OAuth dynamically can authenticate the user providing a more secure way to login.

### 3. **Update mcpServers.json**

Open the [`mcpServers.json`](./mcpServers.json) example config file and update:
- **OpenMemory/Cloud:** OPENMEMORY_API_KEY with your key. [Register](https://openmemory.dev) & get [API here](https://app.openmemory.dev/dashboard)
- **Linkedin-my12345:** Composio with your URL that begins with `https://mcp.composio.dev/composio/server`. [Register](https://app.composio.dev/) and get the [URL here](https://mcp.composio.dev/dashboard) 
- **filesystem:** with the correct full paths on your local computer 

## 🚧 MCP's Limitations
Most notable limitations:
- Security: Prompt poisoning, code injection, tool shadowing, cleartext creds. OAuth partly solves this (if your app supports it), also Docker Desktop MCP Toolkit is a better solution than cleartext config with credentials, but still not an enterprise solution.  
- OAuth-only: if your application has a different Auth mechanism, then you're probably going to store your credentials in cleartext.
- Performance: Context-window and token limits. Each MCP Server may expose a dozen of tools. More than 20-50 tools can significantly decrease quality of LLM performance, therefore controlling how many MCP servers used is crucial (and unfortunately a manual task).

# Choose your MCP Client to continue the lesson

- [Anthropic Claude Desktop](./claude-desktop) - for General Public
- [Cursor](./cursor) - for Developers
- [Roo Code (VS Code Extension)](./roocode) - for Developers
- [VS Code Copilot Chat](./vscode) - for Developers

# Optional
Install one Low-Code Agentic RAG builder:
- [Flowise](../flowise-app/) + external [MCP-Flowise Server](https://github.com/matthewhand/mcp-flowise)
- [LangFlow](../langflow/) (MCP Server is build-in)
