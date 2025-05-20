This guide intends to help you get started with AI faster for:
- Day-to-day computer tasks (Flowise)

# Requirenments:
- In your home directory on your local computer create a directory called `flowise-app`.
- Download `.env` and `docker-compose.yaml` from this repositury to the `flowise-app` directory.
- Follow instructions from [README.md](../README.md)
- Find any text document you like. Exmaple: The Adventures of Sherlock Holmes by Arthur Conan Doyle


# Steps

1. Open browser and search for the latest stable version of the ChromaDB `image: chromadb/chroma:1.0.8` and replace the version in the [flowise-app/docker-compose.yaml](docker-compose.yaml) file with the latest version you found in the Docker Hub. Open the docker-compose.yaml file in any text editors of yuor choice. Example: `image: chromadb/chroma:1.0.9`
2. Open browser and search for the latest version of the Flowise `image: flowiseai/flowise:2.2.5` and replace the version in the [flowise-app/docker-compose.yaml](docker-compose.yaml) file with the latest version you found in the Docker Hub. Open the docker-compose.yaml file in any text editors of yuor choice. Example: `image: flowiseai/flowise:2.2.8`

3. Open the `.env` file with any text editor and update PORT=3000 to PORT=3003.

4. Open the terminal and navigate to the `flowise` directory you created in your home directory.
```shell
#Create an empty directory for Flowise config files (note the dot symbol in the name):
mkdir -p ~/.flowise

#In the terminal window (Powershell in Windows), run the following command:
docker compose -f flowise-app/docker-compose.yaml up -d
```

3. Open the browser and navigate to http://localhost:3000

# In the Flowise web interface

## Create Chatflow
1. In the Flowise web interface, click on the "Marketplace" on the left hand sidebar and search "QnA", select "Flowise Docs QnA". In the top right corner of the page, click on the "Use Template" button. 
2. On the Top righ hand side of the page, click on the "Save" button and give it a name like `flow1`. Note on the top left you might see a cercular yellow button "Sync Nodes" with two circular arrows, click on it to sync the nodes and save the flow again.
3. On the top left hand side of the page, click on the blue "Plus" button and in the opened left menu search "Ollama", select "Ollama Embeddings" and drug and drop to the Chatflow canva. In the Ollama Embeddings block set the BASE URL to `http://host.docker.internal:11434` and the MODEL NAME to `mxbai-embed-large`.
4. Replace the current "LocalAI Embeddings" block with the new one you just added.
5. On the top left hand side of the page, click on the blue "Plus" button and in the opened left menu search "Chroma", select "ChromaDB" and drug and drop to the Chatflow canva. In the ChromaDB block set the BASE URL to `http://host.docker.internal:8000` and the Collection Name field to `collection_512d_mxbai_embed_large`.
6. Replace the current "Faiss" block with the new one you just added.
7. On the top left hand side of the page, click on the blue "Plus" button and in the opened left menu search "ChatOpenRouter", drug and drop to the Chatflow canva. In the ChatOpenRouter block set the  Model name to `google/gemini-2.0-flash-lite-001`, click "Additional Parameters" and scroll to the "BasePath", check base path to `https://openrouter.ai/api/v1`.
8. Replace the current "ChatOllama" block with the new one you just added.
9. On the top left hand side of the page, click on the blue "Plus" button and in the opened left menu search "Splitter", and select "Recursive Character Text Splitter" and drug and drop to the Chatflow canva. In the Recursive Character Text Splitter block set the Chunk Size to `1000` and the Chunk Overlap to `200`.
10. Replace the current "Character Text Splitter" block with the new one you just added.
11. Press Save Chatflow on the top right. You should see a green checkmark on the "Chatflow Saved" popup at the bottom left.
12. If the above does not work, you can import my [flowise-app/flow1_Chatflow.json](flow1_Chatflow.json) file in the flowise directory, create a new empty Chatflow: at the top right click on the Gear/Settings button and select "Load Chatflow" and select the `flow1_Chatflow.json` file from the flowise directory. Use this as last resort option only.

### About host.docker.internal
Since Flowise is running in a Docker container, it is conteinerized meaning it is isolated from the host where it is running. Therefore it cannot access the host network directly such as Ollama. As far as Flowise concerned, the Ollama is running on a separate computer. The `host.docker.internal` is a special DNS name that resolves to the internal IP address used by the localhost. This allows the Flowise container to access the host network where it is running. Ollama is running on the host network http://localhost:11434 on your computer and therefore Flowise in a container can access Ollama instead of using `localhost`, we goint to use the `host.docker.internal` DNS name.

## Ingestion
1. Find any text document you like. Exmaple: The Adventures of Sherlock Holmes by Arthur Conan Doyle.
2. Open the flow and upload the file.
3. Find the "Upsert Vector Database"  green cerular button on the top right hand side of the page, click on it and in the opened window press the "Upsert" button.
4. Wait for the ingestion to complete. You should see a green checkmark on the "Run component" button.

## Chat

On the top right hand side of the page, click on the "Chat" button and start chatting with the AI model.
Ask something like `What context do you have?`  or `What is the document is about?`
