This guide intends to help you get started with AI faster for:
- Programming (LangFlow)

# Requirenments:
- Follow instructions from [README.md](../README.md)
- Install [Visual Studio Code](https://code.visualstudio.com/download) (VS Code) 
- Install [uv](https://docs.astral.sh/uv/getting-started/installation/) on your computer using the [instructions](#uv-installation) below
- Once Docker Desktop app is installed, open it in the top center search bar type "Chromadb" and select "Chroma" and click on the "Run" button, on the popup "Run a new container" window expand the "Optional Settings" and in the "Container Name" enter `chromadb`, and in the Ports section set "Host port" to `8000` and click on the "Run" button.
- Install the [Git CLI](#cli-tools) in your operation system.

# CLI tools
Command Line Interface (CLI) tools are used to interact with your computer's operating system and perform various tasks in a terminal by typing commands.
Follow one of the instructions below to install the Git CLI tool in your operating system. Choose one based on your OS:

## Windows
Install [winget cli](https://github.com/microsoft/winget-cli) package manager via Microsoft Store > [App Installer](https://apps.microsoft.com/detail/9nblggh4nns1).
Open Powershell application. Then run the following command in the terminal window:
```shell
winget install --id Git.Git -e
```

## Ubuntu Linux
The `apt` package manager is installed by default.
Open terminal application. Then run the following command in the terminal window:
```shell
apt install git
```

## macOS
Open terminal application.
Install [brew cli](https://brew.sh/) package manager by copying & pasting the command from the website into the terminal and hit enter to execute it.
Then run the following command in the terminal window:
```shell
brew install git
```

## UV Installation:

### macOS & Linux
Open terminal application. Then run the following command in the terminal window:
```shell
curl -sSfL https://get.uv.sh | sh
```
if `curl` is not installed, install it with `apt install curl` on linux or `brew install curl` on macOS.

### Windows:
Open Powershell application. Then run the following command in the terminal window:
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | more"
```

## LangFlow Installation:
Open terminal application. Then run the following command in the terminal window:
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
In the VS Code window, open the terminal by pressing `Ctrl + Shift + \` or selecting `Terminal > New Terminal` from the menu bar or by pressing Toggle Terminal from the bottom panel on the top right. Then run the following command in the terminal window:
```shell
# initialize uv in the current directory
uv init --python 3.12 .
# create a virtual environment in the current directory
uv venv --python 3.12
# activate the virtual environment in the current directory
source .venv/bin/activate
```

This creates so-colled virtual environment for Python in the current directory. Virtual environment is a tool that helps to keep dependencies required by different projects separate by creating isolated python environments for them. This is especially useful when working with LangFlow as it has many dependencies that may conflict with other projects you have on your computer.

### LangFlow Dependencies Installation:
Open the `langflow/.env.example` file and copy all the lines into a new file called `.env` in the langflow directory of the project.

Then execute the following commands in the terminal window:
```shell
# install all the modules from requirements.txt file in the langflow directory
uv pip install -r langflow/requirements.txt 

# try this if the above command fails
#uv pip install langflow --force-reinstall

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

# We set the port to 7860 on local computer and using the .env file in the langflow directory
langflow run --host 0.0.0.0 --port 7860 --env-file langflow/.env
# Wait for the server to start and then open the browser, it can take a minute. It'll display a message like this when ready:
# Welcome to Langflow
# 🟢 Open Langflow → http://0.0.0.0:7860

# We are ready to go! Open the browser and navigate to http://localhost:7860
```
### Update LangFlow version
Now lets find most recent [langflow](https://github.com/langflow-ai/langflow) version in the Release section. For example you might see `1.4.2`. now replace the version in the `langflow===1.4.1` line in the `langflow/requirements.txt` file with the latest version you found in the Release section. If the langflow running, interrupt it with `CTRL + C`. Then run the following command in the terminal window:
```shell
source .venv/bin/activate
# install all the modules from requirements.txt file in the langflow directory
uv pip install -r langflow/requirements.txt 
# And run the langflow again.
langflow run --host 0.0.0.0 --port 7860 --env-file langflow/.env
```


### Working with LangFlow in Browser

#### Simple Scenario
RAG stands for Retrieval-Augmented Generation. It is a technique that combines the power of searching chunks (blocks of text, think of them as paragraphs) of documents with AI models to improve the results of language tasks.

1. Open browser and navigate to http://localhost:7860
2. Press create Flow
3. Select "Vector Store RAG"
4. In the left hand side, expand "Components" and search for Ollama, then drag "Ollama Embeddings" and replace OpenAI Embeddings blocks. Check if ollama application is running by running `ollama ps` command in your terminal and you should see an empty list.
5. In the Ollama Embedding block, set the BASE URL to `http://localhost:11434` and the MODEL NAME to `mxbai-embed-large`
6. Create OpenAI-compatible block for OpenRouter: On the flow canvas, look to the OpenAI block, hover over with mouse and select from the poped up menu ontop "Controls", scroll to the "OpenAI API Base" and toggle the Swow button, close and in the text box "OpenAI API Base" in the OpenAI blockenter `https://openrouter.ai/api/v1` and also populate the "OpenAI API Key" text block with your API key you created earlier in the OpenRouter website.
7. In the left hand side, expand "Components" and search for Chroma, then drag "Chroma DB" from the Vector Stores and replace DS Astra DB blocks.
8. In each Chroma Block, hover over with mouse and select from the poped up menu ontop "Controls", scroll to the "Server Host", "Server HTTP Port", "Server SSL Enabled" and toggle the Swow button for each, close and in the text box "Server Host" in the Chroma block enter `localhost` and in the "Server HTTP Port" enter `8000` (From Docker Desktop) and in the "Server SSL Enabled" enter `false` and set the "Collection Name" to `collection_512d_mxbai_embed_large`.
9. Go to the "OpenRouter.ai" and search for the "Google: Gemini 2.0 Flash Lite", copy the model API name that should start like `google/gemini-2.0-flash-lite...`, we will use it later to paste into the "Model Name" text box in the OpenAI block.
10. In the OpenAI block, hover over with mouse and select from the poped up menu ontop "Code", scroll to the "DropdownInput" that starts "model_name": Replace "DropdownInput" with "StrInput" and remove the "options", "combobox" and "real_time_refresh" lines, replace `value=OPENAI_MODEL_NAMES[1],` with empty string `value=""`. Close the code by pressing "Check & Save" button. Paste the previously copied Gemini model API name into the "Model Name" text box in the OpenAI block.
11. If the steps do not work for you, you can import my [Vector_Store_RAG.json](Vector_Store_RAG.json) file in the langflow directory: create a new Blank flow, at the top center next to the flow name "Untitled document" click on the down arrow button and select "Import" and choose the `Vector_Store_RAG.json` file from the langflow directory. Use this as last resort option only.

Here is an example of snippet to modify:
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
Example of how modified resulting code should look like:
```python
        StrInput(
            name="model_name",
            display_name="Model Name",
            advanced=False,
            value=""
        ),
```

#### Ingestion
Check if ollama application is running by running `ollama ps` command in your terminal and you should see an empty list. It will be populated with a name of currently or recentry running local models.

Before we start running this flow in playground we need to ingest some data into the vector store. 

1. Find any text document you like. Exmaple: The Adventures of Sherlock Holmes by Arthur Conan Doyle.
2. Open the flow and upload the file.
3. Find the "Load dataflow" follow connections all the way to the Vector DB block and click on the "Run component" play button.

**Issue**: `Error Building Component. Error building Component File: File or directory not found: ~/.langflow/077f0788-658c-4ee3-8966-b65f594f81e4/6e7e7cff-5288-49a7-9c6f-7e4c221cb805.txt` 
**Workaround**: In the LangFlow UI press top right bell button to see the error and the full file path. Open the file in the error message `code ~/.langflow/077f0788-658c-4ee3-8966-b65f594f81e4/6e7e7cff-5288-49a7-9c6f-7e4c221cb805.txt` and copy paste text into this file from the downloaded [file](../pg1661.txt).

#### Playground
Check if ollama application is running by running `ollama ps` command in your terminal and you should see an empty list.
In the playground, you can now ask questions about the data you ingested. For example, you can ask "What are the names of the characters in the book?" and the AI model will answer based on the data in the vector store. 


### Stopping LangFlow
When done with the langflow, you can stop the server by pressing `CTRL + C` in the terminal window where it is running (the one that displays the message below):
```
Welcome to Langflow
🟢 Open Langflow → http://0.0.0.0:7860
```