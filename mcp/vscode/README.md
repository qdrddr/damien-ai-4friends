# 🧠 Learning Lesson: Getting Started with MCP Using VS Code GitHub Copilot Chat

## 🚀 What You'll Learn

By the end of this lesson, you'll be able to:

- Set up **VS Code GitHub Copilot Chat** as an MCP Client
- Connect VS Code GitHub Copilot Chat to local and cloud-based MCP Servers
- Will take approximately 15 minutes

## 🖥️ VS Code GitHub Copilot Chat

**VS Code GitHub Copilot Chat** is a developer-oriented IDE with built-in LLM support and native MCP Client functionality. It supports:
- `STDIO`, `SSE` and `streamable-HTTP` transport protocols
- Run local servers with NPM, PIP, Docker or by running a local command
- No dedicated Global MCP configuration file, MCP is bundled with the VS Code other Settings
- Dedicated MCP Config project-based saves config to `.vscode/mcp.json` 
- Direct integration with popular local MCP servers

Other supported developer-oriented MCP clients include: Cursor, Windsur, Roo Code, Cline, Continue (vary in transport & config support).

---

## How to Set Up MCP with VS Code GitHub Copilot Chat

### 1. **Install VS Code**
Go to [Code.VisualStudio.com](https://code.visualstudio.com/Download) and install the app for your OS.

### 2. **Install GitHub Copilot Chat**
Go to [Marketplace.VisualStudio](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) and install the GitHub Copilot Chat Extension for your VS Code IDE. Alternatively use the Extension button in VS Code on the left hand side (the four cubes icon with one of the top right cubes falling off) and search for GitHub Copilot Chat. Press the `Install` button.

### 3. **Local MCP Servers Requirements**
In the previous guide you prepared by installing these utils, if you didn't, follow the previous step in [README.md](../):
- With `uv`, `npm`, `pip`, `node`, `docker`.
- Standalone Containers (may support STDIO, SSE or even Streamable-HTTP)
- Via MCP Toolkit from Docker Desktop extension (supports STDIO protocol only)

#### 3.1 **Cloud MCP Servers**
Some online services have native MCP support (e.g. GitHub, Cloudflare).
- https://api.githubcopilot.com/mcp/ (streamable-HTTP only, requires Authentication, [read more](https://github.com/github/github-mcp-server))
- https://docs.mcp.cloudflare.com/sse (SSE transport only, no Auth), see [other Cloudflare's own MCP servers here](https://developers.cloudflare.com/agents/model-context-protocol/mcp-servers-for-cloudflare/).
- https://mcp.deepwiki.com/sse (SSE transport only, no Auth)

### 4. **Open VS Code & Create a project**
- Create an empty folder on your computer
- Start VS Code app and open the recently created folder

### 5. **⚙️ VS Code Copilot Chat UI**

<img src="./1_vscode_mcp.gif" alt="VS Code Copilot Chat UI" width="300">

- Open VS Code
- On the top middle there's a search bar, right to the search bar should appear GitHub Copilot button, when hover over "Toggle Chat", press the button
- At the right bottom select "Agent" (instead of the Ask/Edit), click on the Tools button, when hover over "Configure Tools"
- From the top center search bar you'll see a list opened, scroll to the very bottom 
- Press "+ Add More Tools" 
- Press "+ Add MCP Server"

The Workspace Settings for project-based MCP config will only apply those MCP Servers for your currently opened workspace. While the "User Settings" installed MCP Servers will be used by VS Code GitHub Copilot Chat across all your projects.

### 6. **Transport Protocol**

#### **6.1 STDIO**
- After completing step #5, choose Command (STDIO), enter this command `npx -y @modelcontextprotocol/server-filesystem "/Users/username/Desktop" "/path/to/other/allowed/dir"`
- Press Enter
- Then give a name for this MCP Server `filesystem`
- Choose if you wish to add this MCP Server Globally (User Settings) or to this project only (Workspace Settings - saves into `.vscode/mcp.json`)
- Observe the opened `settings.json` file, scroll down to the `"mcp":`

Alternatively add `docker run -i --rm alpine/socat STDIO TCP:host.docker.internal:8811` command. (You need to have installed Docker Desktop and the MCP Toolkit extension).

#### **6.2 SSE**
`/sse` at the end indicates that transport protocol is SSE. 
- After completing step #5, choose HTTP (HTTP or Server-Side-Events), enter this command `https://mcp.deepwiki.com/sse`
- Press Enter
- Then give a name for this MCP Server `deepwiki`
- Choose if you wish to add this MCP Server Globally (User Settings) or to this project only (Workspace Settings - saves into `.vscode/mcp.json`)
- Observe the opened `settings.json` file, scroll down to the `"mcp":`

#### **6.3 streamable-HTTP**
`/mcp` at the end typically indicates that transport protocol is streamable-HTTP. 
- After completing step #5, choose HTTP (HTTP or Server-Side-Events), enter this command `https://mcp.context7.com/mcp`
- Press Enter
- Then give a name for this MCP Server `context7`
- Choose if you wish to add this MCP Server Globally (User Settings) or to this project only (Workspace Settings - saves into `.vscode/mcp.json`)
- Observe the opened `settings.json` file, scroll down to the `"mcp":`

#### **6.4 NPM Package**
- After completing step #5, choose NPM Package, enter this command `@netlify/mcp`
- Press Enter
- Press Allow
- Then give a name for this MCP Server `netlify`
- Choose if you wish to add this MCP Server Globally (User Settings) or to this project only (Workspace Settings - saves into `.vscode/mcp.json`)
- Observe the opened `settings.json` file, scroll down to the `"mcp":`

Alternatively add `@modelcontextprotocol/server-filesystem` command. After you add this command, you'll have to modify the default placeholders `/Users/username/Desktop` & `/path/to/other/allowed/dir` for this MCP Server to correctly work.

#### **6.5 PIP Package**
- After completing step #5, choose PIP Package, enter this command `mcp-server-time`
- Press Enter
- Press Allow
- Then give a name for this MCP Server `time`
- Choose if you wish to add this MCP Server Globally (User Settings) or to this project only (Workspace Settings - saves into `.vscode/mcp.json`)
- Observe the opened `settings.json` file, scroll down to the `"mcp":`

#### **6.6 Docker Image**
- After completing step #5, choose Docker Image, enter this command `mcp/fetch`
- Press Enter
- Then give a name for this MCP Server `fetch`
- Choose if you wish to add this MCP Server Globally (User Settings) or to this project only (Workspace Settings - saves into `.vscode/mcp.json`)
- Observe the opened `settings.json` file, scroll down to the `"mcp":`

### **8. Alternatively modify settings.json**
Instead of following all the steps from #6 you can manually modify the VS Code settings.json config file for global (User Settings):

- On the bottom left press the gear button and select Settings
- In the Search bar of the Settings window type "mcp"
- Under "Features" press "Chat", and press "Edit in settings.json"
- In the first curly bracket look for the `"mcp": { "servers": { } }` if it doesn't exist, add at the very beginning right after the first opening curly bracket.
- If not certain, consider first performing step 6.1 that will create the necessary setting
- Once the `"mcp": { "servers": { } }` found, now you can manually add mcp settings directly into the settings.json

### **9. Alternatively modify .vscode/mcp.json**
Instead of following all the steps from #6 you can manually modify the `.vscode/mcp.json` config file for project (Workspace Settings):

- In current project create a folder `.vscode` (note dot at the beginning is a must)
- Create a new file `mcp.json` in the `.vscode` folder
- Copy from [`mcpServers.json`](../mcpServers.json)
- Replace "mcpServers" with "servers"

Example of `.vscode/mcp.json`:
```json
{
  "servers": {
    "fetch": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "mcp/fetch"
      ]
    }
  }
}
```
