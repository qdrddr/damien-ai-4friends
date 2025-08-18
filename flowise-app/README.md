This guide is intended to help you get started with AI faster for:
- Day-to-day computer tasks (Flowise)
- You might need a mouse for this ;)

# Requirements:
- In your home directory on your local computer, create a directory called `flowise-app`.
- Download the `.env` and `docker-compose.yaml` files from this repository to the `flowise-app` directory.
- Follow the instructions from [README.md](../README.md).
- Find any text document you like. Example: The Adventures of Sherlock Holmes by Arthur Conan Doyle.

# Steps

1. Open your browser and search for the [latest stable version of ChromaDB](https://hub.docker.com/r/chromadb/chroma/tags) `image: chromadb/chroma:1.0.8` and replace the version (tag) in the [flowise-app/docker-compose.yaml](docker-compose.yaml) file with the latest version you found on Docker Hub. Open the docker-compose.yaml file in any text editor of your choice. Example: `image: chromadb/chroma:1.0.9`
2. Open your browser and search for the [latest version of Flowise](https://hub.docker.com/r/flowiseai/flowise/tags) `image: flowiseai/flowise:2.2.5` and replace the version (tag) in the [flowise-app/docker-compose.yaml](docker-compose.yaml) file with the latest version you found on Docker Hub. Open the docker-compose.yaml file in any text editor of your choice. Example: `image: flowiseai/flowise:2.2.8`
3. Open the `.env` file with any text editor and update `PORT=3000` to `PORT=3003`.
4. Open the terminal and navigate to the `flowise-app` directory you created in your home directory.
```shell
# Create an empty directory for Flowise *config files* (note the dot symbol in the name):
mkdir -p ~/.flowise

# In the terminal window (Powershell on Windows), run the following command:
docker compose -f flowise-app/docker-compose.yaml up -d
```
5. Open your browser and navigate to http://localhost:3003

# In the Flowise web interface

## Create Chatflow
1. In the Flowise web interface, click on "Marketplace" on the left-hand sidebar and search for "QnA". Select "Flowise Docs QnA". In the top right corner of the page, click the "Use Template" button.
2. On the top right-hand side of the page, click the "Save" button and give it a name like `flow1`. Note: on the top left you might see a circular yellow button "Sync Nodes" with two circular arrows; click on it to sync the nodes and save the flow again.
3. On the top left-hand side of the page, click the blue "Plus" button and in the opened left menu, search for "Ollama". Select "Ollama Embeddings" and drag and drop it to the Chatflow canvas. In the Ollama Embeddings block, set the BASE URL to `http://host.docker.internal:11434` and the MODEL NAME to `mxbai-embed-large` (`ollama list`).
4. Replace the current "OpenAI Embeddings" block with the new one you just added.
5. On the top left-hand side of the page, click the blue "Plus" button and in the opened left menu, search for "Chroma". Select "ChromaDB" and drag and drop it to the Chatflow canvas. In the ChromaDB block, set the Chroma URL to `http://host.docker.internal:8000` and the Collection Name field to `collection_512d_mxbai_embed_large`.
6. Replace the current "Faiss" or "In-Memory Vector Store" block with the new one you just added.
7. On the top left-hand side of the page, click the blue "Plus" button and in the opened left menu, search for "ChatOpenRouter". Drag and drop it to the Chatflow canvas. In the ChatOpenRouter block, set the Model name to `google/gemini-2.0-flash-lite-001`, click "Additional Parameters" and scroll to "BasePath". Set BasePath to `https://openrouter.ai/api/v1`. Add your OpenRouter API key. 
8. Replace the current "ChatOllama" or ChatOpenAI block with the new one you just added.
9. On the top left-hand side of the page, click the blue "Plus" button and in the opened left menu, search for "Splitter", and select "Recursive Character Text Splitter". Drag and drop it to the Chatflow canvas. In the Recursive Character Text Splitter block, set the Chunk Size to `1000` and the Chunk Overlap to `200`.
10. Replace the current "Character Text Splitter" block with the new one you just added.
11. Press "Save Chatflow" on the top right. You should see a green checkmark in the "Chatflow Saved" popup at the bottom left.
12. If a File node is missing, on the top left-hand side of the page, click the blue "Plus" button and in the opened left menu, search for "File". Drag and drop it to the Splitter and connect the two.
13. If the above does not work, you can import my [flowise-app/flow1_Chatflow.json](flow1_Chatflow.json) file in the flowise directory. Create a new empty Chatflow: at the top right, click the Gear/Settings button and select "Load Chatflow" and select the `flow1_Chatflow.json` file from the flowise directory. Use this as a last resort only.

### About host.docker.internal
Since Flowise app is running in a Docker container, it is containerized, meaning it is isolated from the host where it is running. Therefore, it cannot access the host network directly, such as Ollama. As far as Flowise is concerned, Ollama is running on a separate computer. The `host.docker.internal` is a special DNS name that resolves to the internal IP address used by Ollama on localhost. This allows the Flowise container to access the host where it is running and access it via network. Ollama is running on the host network at http://localhost:11434 on your computer, and therefore Flowise in a container can access Ollama by using the `host.docker.internal` DNS name instead of `localhost`.

## Ingestion Pipeline
This pipeline executed by the developer to add data to a database. Later that data will be used by the chat pipeline:
1. Find any text document you like. Example: The Adventures of Sherlock Holmes by Arthur Conan Doyle.
2. Open the flow and upload the file.
3. Find the "Upsert Vector Database" green circular button on the top right-hand side of the page, click on it, and in the opened window press the "Upsert" button.
4. Wait for the ingestion to complete. You should see a green checkmark on the "Run component" button.

## Chat Pipeline
This pipeline executed each time a user ask a question in the chat:
1. On the top right-hand side of the page, click on the "Chat" button and start chatting with the AI model.
2. Ask something like `What context do you have?` or `What is the document about?`
