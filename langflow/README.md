This guide is intended to help you get started with AI faster for:
- Programming (LangFlow)

# Requirements:
- Follow the instructions from [README.md](../README.md)
- Install [Visual Studio Code](https://code.visualstudio.com/download) (VS Code)
- Install [uv](https://docs.astral.sh/uv/getting-started/installation/) on your computer using the [instructions](#uv-installation) below
- Once Docker Desktop is installed, open it. In the top center search bar, type "Chromadb", select "Chroma", and click the "Run" button. In the popup "Run a new container" window, expand the "Optional Settings". In the "Container Name" field, enter `chromadb`, and in the Ports section, set "Host port" to `8000`, then click the "Run" button.
- Install the [Git CLI](#cli-tools) on your operating system.

# CLI Tools
Command Line Interface (CLI) tools are used to interact with your computer's operating system and perform various tasks in a terminal by typing commands.
Follow one of the instructions below to install the Git CLI tool on your operating system. Choose one based on your OS:

## Windows
Install the [winget CLI](https://github.com/microsoft/winget-cli) package manager via Microsoft Store > [App Installer](https://apps.microsoft.com/detail/9nblggh4nns1).
Open the Powershell application. Then run the following command in the terminal window:
```shell
winget install --id Git.Git -e
```

## Ubuntu Linux
The `apt` package manager is installed by default.
Open the terminal application. Then run the following command in the terminal window:
```shell
apt install git
```

## macOS
Open the terminal application.
Install the [brew CLI](https://brew.sh/) package manager by copying & pasting the command from the website into the terminal and hitting enter to execute it.
Then run the following command in the terminal window:
```shell
brew install git
```

## UV Installation:

### macOS & Linux
Open the terminal application. Then run the following command in the terminal window:
```shell
curl -sSfL https://get.uv.sh | sh
```
If `curl` is not installed, install it with `apt install curl` on Linux or `brew install curl` on macOS.

### Windows:
Open the Powershell application. Then run the following command in the terminal window:
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | more"
```

## LangFlow Installation:
Open the terminal application. Then run the following commands in the terminal window:
```shell
mkdir -p ~/git
cd ~/git
git clone https://github.com/qdrddr/damien-ai-4friends
cd ~/git/damien-ai-4friends
# print the current directory
pwd

# open Visual Studio Code in the current directory
code .
```

### UV Init:
In the VS Code window, open the terminal by pressing `Ctrl + Shift + \` or selecting `Terminal > New Terminal` from the menu bar, or by pressing Toggle Terminal from the bottom panel on the top right. Then run the following commands in the terminal window:
```shell
# initialize uv in the current directory
uv init --python 3.12 .
# create a virtual environment in the current directory
uv venv --python 3.12
# activate the virtual environment in the current directory
source .venv/bin/activate
```

This creates a so-called virtual environment for Python in the current directory. A virtual environment is a tool that helps keep dependencies required by different projects separate by creating isolated Python environments for them. This is especially useful when working with LangFlow, as it has many dependencies that may conflict with other projects you have on your computer.

### LangFlow Dependencies Installation:
Open the `langflow/.env.example` file and copy all the lines into a new file called `.env` in the langflow directory of the project.

Then execute the following commands in the terminal window:
```shell
# install all the modules from requirements.txt file in the langflow directory
uv pip install -r langflow/requirements.txt 

# try this if the above command fails
# uv pip install langflow --force-reinstall

# This command creates a unique secret key for your LangFlow installation and just prints it to the terminal
python3 -c "from secrets import token_urlsafe; print(f'LANGFLOW_SECRET_KEY={token_urlsafe(32)}')"
# example: LANGFLOW_SECRET_KEY=3eRZyTDfQiXXXXXlzucVXftK4yaKtL6npWQNbMnh2Zo
```

Copy the secret key that starts with `LANGFLOW_SECRET_KEY=` and paste it into the `.env` file in the langflow directory of the project.
Find the line that starts with `LANGFLOW_SECRET_KEY=` and replace the value with the secret key you generated above.

### LangFlow Execution:
```shell
# run the langflow server
source .venv/bin/activate
mkdir -p ~/.langflow

# We set the port to 7860 on the local computer and use the .env file in the langflow directory
langflow run --host 0.0.0.0 --port 7860 --env-file langflow/.env
# Wait for the server to start and then open the browser; it can take a minute. It'll display a message like this when ready:
# Welcome to Langflow
# 🟢 Open Langflow → http://0.0.0.0:7860

# We are ready to go! Open the browser and navigate to http://localhost:7860
```
### Update LangFlow Version
Now let's find the most recent [langflow](https://github.com/langflow-ai/langflow) version in the Release section. For example, you might see `1.4.2`. Now replace the version in the `langflow===1.4.1` line in the `langflow/requirements.txt` file with the latest version you found in the Release section. If LangFlow is running, interrupt it with `CTRL + C`. Then run the following commands in the terminal window:
```shell
source .venv/bin/activate
# install all the modules from requirements.txt file in the langflow directory
uv pip install -r langflow/requirements.txt 
# And run LangFlow again.
langflow run --host 0.0.0.0 --port 7860 --env-file langflow/.env
```


### Working with LangFlow in the Browser

#### Simple Scenario
RAG stands for Retrieval-Augmented Generation. It is a technique that combines the power of searching chunks (blocks of text, think of them as paragraphs) of documents with AI models to improve the results of language tasks.

1. Open your browser and navigate to http://localhost:7860
2. Press "Create Flow"
3. Select "Vector Store RAG"
4. On the left-hand side, expand "Components" and search for Ollama, then drag "Ollama Embeddings" and replace the OpenAI Embeddings blocks. Check if the Ollama application is running by running `ollama ps` in your terminal; you should see an empty list.
5. In the Ollama Embedding block, set the BASE URL to `http://localhost:11434` and the MODEL NAME to `mxbai-embed-large`.
6. Create an OpenAI-compatible block for OpenRouter: On the flow canvas, look for the OpenAI block, hover over it with your mouse, and select from the popup menu on top "Controls". Scroll to the "OpenAI API Base" and toggle the Show button. Close, and in the text box "OpenAI API Base" in the OpenAI block, enter `https://openrouter.ai/api/v1` and also populate the "OpenAI API Key" text box with your API key you created earlier on the OpenRouter website.
7. On the left-hand side, expand "Components" and search for Chroma, then drag "Chroma DB" from the Vector Stores and replace the DS Astra DB blocks.
8. In each Chroma Block, hover over it with your mouse and select from the popup menu on top "Controls", scroll to "Server Host", "Server HTTP Port", and "Server SSL Enabled" and toggle the Show button for each. Close, and in the text box "Server Host" in the Chroma block, enter `localhost`, in the "Server HTTP Port" enter `8000` (from Docker Desktop), in the "Server SSL Enabled" enter `false`, and set the "Collection Name" to `collection_512d_mxbai_embed_large`.
9. Go to "OpenRouter.ai" and search for "Google: Gemini 2.0 Flash Lite". Copy the model API name that should start like `google/gemini-2.0-flash-lite...`; we will use it later to paste into the "Model Name" text box in the OpenAI block.
10. In the OpenAI block, hover over it with your mouse and select from the popup menu on top "Code". Scroll to the "DropdownInput" that starts "model_name": Replace "DropdownInput" with "StrInput" and remove the "options", "combobox", and "real_time_refresh" lines. Replace `value=OPENAI_MODEL_NAMES[1],` with an empty string `value=""`. Close the code by pressing the "Check & Save" button. Paste the previously copied Gemini model API name into the "Model Name" text box in the OpenAI block.
11. If the steps do not work for you, you can import my [Vector_Store_RAG.json](Vector_Store_RAG.json) file in the langflow directory: create a new blank flow, at the top center next to the flow name "Untitled document" click on the down arrow button and select "Import" and choose the `Vector_Store_RAG.json` file from the langflow directory. Use this as a last resort option only.

Here is an example of a snippet to modify:
```python
        DropdownInput(
            name="model_name",
            display_name="Model Name",
            advanced=False,
            options=OPENAI_MODEL_NAMES + OPENAI_REASONING_MODEL_NAMES,
            value=OPENAI_MODEL_NAMES[1],
            combobox=True,
            real_time_refresh=True,
        ),
```
Example of how the modified resulting code should look:
```python
        StrInput(
            name="model_name",
            display_name="Model Name",
            advanced=False,
            value=""
        ),
```

#### Ingestion
Check if the Ollama application is running by running `ollama ps` in your terminal; you should see an empty list. It will be populated with the name of currently or recently running local models.

Before we start running this flow in the playground, we need to ingest some data into the vector store.

1. Find any text document you like. Example: The Adventures of Sherlock Holmes by Arthur Conan Doyle.
2. Open the flow and upload the file.
3. Find the "Load dataflow" block, follow connections all the way to the Vector DB block, and click on the "Run component" play button.

**Issue**: `Error Building Component. Error building Component File: File or directory not found: ~/.langflow/077f0788-658c-4ee3-8966-b65f594f81e4/6e7e7cff-5288-49a7-9c6f-7e4c221cb805.txt` 
**Workaround**: In the LangFlow UI, press the top right bell button to see the error and the full file path. Open the file in the error message `code ~/.langflow/077f0788-658c-4ee3-8966-b65f594f81e4/6e7e7cff-5288-49a7-9c6f-7e4c221cb805.txt` and copy-paste text into this file from the downloaded [file](../pg1661.txt).

#### Playground
Check if the Ollama application is running by running `ollama ps` in your terminal; you should see an empty list.
In the playground, you can now ask questions about the data you ingested. For example, you can ask "What are the names of the characters in the book?" and the AI model will answer based on the data in the vector store.


### Stopping LangFlow
When done with LangFlow, you can stop the server by pressing `CTRL + C` in the terminal window where it is running (the one that displays the message below):
```
Welcome to Langflow
🟢 Open Langflow → http://0.0.0.0:7860
```