Thi sguide intends to help you get started with AI faster for:
- Programming ([LangFlow](langflow/README.md))
- Day-to-day computer tasks ([Flowise](flowise-app/README.md))

# Requirenments:
1. [Download & Install Docker Desktop](https://www.docker.com/products/docker-desktop/) ([doc](https://docs.docker.com/get-started/get-docker/)).
2. Once Docker Desktop app is installed, open it in the top center search bar type "Chromadb" and select "Chroma" and click on the "Run" button, on the popup "Run a new container" window expand the "Optional Settings" and in the "Container Name" enter `chromadb`, and in the Ports section set "Host port" to `8000` and click on the "Run" button.
3. Register with [OpenRouter](https://openrouter.ai/settings/credits) & add $5 credits, [create a Key](https://openrouter.ai/settings/keys).
4. Install [Ollama](https://ollama.com/download), then go to the [Models](https://ollama.com/search) and select "Embedding", choose `mxbai-embed-large`, note there's "View all →" link on the top right of the "Models" table, select `mxbai-embed-large:latest`, then copy command that starts `ollama pull mxbai...` and paste into your terminal and hit enter to execute it. Check if ollama is running by running `ollama list` command in your terminal and you should see `mxbai-embed-large` in the list. This will install the embedding model and download it to your computer locally.
5. Install the [Git CLI](#cli-tools) in your operation system.
6. Download any text document you like. Exmaple: [The Adventures of Sherlock Holmes by Arthur Conan Doyle](https://www.gutenberg.org/ebooks/1661) Plain text and save to you local computer. 


