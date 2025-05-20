This guide for all those who want to get started with AI faster:
- Programming ([LangFlow](langflow/README.md))
- Day-to-day computer tasks ([Flowise](flowise-app/README.md))

# Requirenments:
0. Read my [blog post on Medium](https://medium.com/@qdrddr/1a3393e0c3c9) to understand what RAG is and how it works.
1. [Download & Install Docker Desktop](https://www.docker.com/products/docker-desktop/) ([doc](https://docs.docker.com/get-started/get-docker/)).
2. Register with [OpenRouter](https://openrouter.ai/settings/credits) & add $5 credits, [create a Key](https://openrouter.ai/settings/keys).
3. Install [Ollama](https://ollama.com/download), then go to the [Models](https://ollama.com/search) and select "Embedding", choose `mxbai-embed-large`, note there's "View all →" link on the top right of the "Models" table, select `mxbai-embed-large:latest`, then copy command that starts `ollama pull mxbai...` and paste into your terminal and hit enter to execute it. Check if ollama is running by running `ollama list` command in your terminal and you should see `mxbai-embed-large` in the list. This will install the embedding model and download it to your computer locally.
4. Download any text document you like. Exmaple: [The Adventures of Sherlock Holmes by Arthur Conan Doyle](pg1661.txt) Plain text and save to you local computer.
5. Continue with [LangFlow](langflow/README.md) if you are a developer or [Flowise](flowise-app/README.md) if you want to use no-code approach.


