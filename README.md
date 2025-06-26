This guide is for anyone who wants to get started with AI quickly:
- Programming ([LangFlow](langflow/))
- Day-to-day computer tasks ([Flowise](flowise-app/))
- Model Context Protocol: [MCP Clinets, Proxy & Servers](mcp/)

Please ⭐️ Star this repo 😉

# Low-Code Requirements:
0. Read my [blog post on Medium](https://medium.com/@qdrddr/1a3393e0c3c9) to understand the basics of RAG and how it works.
1. [Download & Install Docker Desktop](https://www.docker.com/products/docker-desktop/) ([docs](https://docs.docker.com/get-started/get-docker/)).
2. Register with [OpenRouter](https://openrouter.ai/settings/credits), add $5 in credits, and [create an API Key](https://openrouter.ai/settings/keys).
3. Install [Ollama](https://ollama.com/download). Then go to the [Models](https://ollama.com/search) page and select "Embedding". Choose `mxbai-embed-large` (note the "View all →" link at the top right of the "Models" table), select `mxbai-embed-large:latest`, then copy the command that starts with `ollama pull mxbai...`, paste it into your terminal, and hit enter to execute it. Check if Ollama is running by running the `ollama list` command in your terminal; you should see `mxbai-embed-large` in the list. This will install and download the embedding model to your computer locally.
4. Download any text document you like. Example: [The Adventures of Sherlock Holmes by Arthur Conan Doyle](pg1661.txt) (plain text) and save it to your local computer.
5. Continue with [LangFlow](langflow/) if you are a developer, or [Flowise](flowise-app/) if you want to use a no-code approach.


# MCP Practical Guide
0. Read my [blog post on Medium](https://medium.com/@qdrddr/0c02f3915867) to understand the basics of MCP and how it works.
1. Continue with [MCP lessons](mcp/)