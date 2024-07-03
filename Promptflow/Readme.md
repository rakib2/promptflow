# Stater Project Promptflow
This is the starter project for Promptflow projects. Here we will set up the development enviornment and initiate a basic promptflow project. In general, we will use python and Visual Studio Code is the recommended IDE.


## Setup of environment

### Python

To be able to execute this environment, one has to have python installed and enabled. It is recommended to use virtual environments (see https://realpython.com/python-virtual-environments-a-primer/).

##### Windows

For Windows, you can create virtual environment  with the command: `python -m venv venv`
And activate it with the command: `./venv/Scripts/activate`

Afterwards one has to install the required python packages with the following command: `pip install -r requirements_windows.txt`

##### macOS

For MacBook users, you can create virtual environment with the command: `python3 -m venv .venv`. After running the command you should be able to see directory `.venv` in the root project. DO NOT COMMIT the new folder.
Next step is to activate your environment with the command: `source .venv/bin/activate`

After that, you can proceed to installing required python packages with the following command: `pip3 install -r requirements_mac.txt`

Once completed, you should be fine python-wise.

### API-Keys and endpoints
Promptflow right now does not support the usage of custom headers as needed for the API-Management, which is the reason why we will connect directly to the Azure-OpenAI-Resources in our resource group.

For this project, the credentials have to be specified in two places:
- in the .env-file: Please copy the .sample.env file to .env and enter your credentials there. This file is not checked in into git and should never be.
- a connection, which has to be created with the `pf`-cli. You can do this using `pf connection create -f connections/azure_openai.yml` where you will be prompted to enter the API-Key.

In general, the principle is to never deploy new OpenAI-Resources. There are common resources in the common resource group available, like azure cognitive search.
For your personal non-AI-deployments (servers and whatever you need), please use the joint resource group `rg-training-sdlc-july24` and name the resources you create after your team, e.g. `Zurich-Team-1-VM`. For any other questions, please refer to the manual of `sabin.bhandari@avanade.com` (sent in the general chat).

### IDE-Setup
Install the Promptflow extension in Visual Studio Code (prompt-flow.prompt-flow, see recommended extensions).

## VERY Brief overview over the promtpflow framework
For a more detailed guide, please refer to the [official documentation](https://microsoft.github.io/promptflow/concepts/index.html)

Promptflow consistes out of Flows, Tools and Connections: 
- Flows are the actual definitions of the chatbots. You can either define a flex flow in python or a DAG-flow using YAML and the Promptflow-Plugin in VS Code.
- There are three basic tools available: LLM,  Python (custom python functions) & Prompt (preparation of complex strings as prompts). Furthermore there are tools from partners available, like a Vector-DB integration.
- Connections are the API-Keys and Endpoints for the AI-Models.

What you want to use depends entirely on your skills and requirements.  


## Executing the examples
- first execute a basic chat example to make sure that the environment is set up correctly for that either execute the command `pf flow test --flow .\examples\basic-chat\ --interactive` or start the basic-chat example in the VS Code Plugin. Make sure that you specified the right connection `azure_openai_connection_yml` for the flow either directly in the yaml (flow.dag.yaml) or in the VS Code Plugin.
- now you can execute the more complex example, e.g. with the command `pf flow test --flow .\examples\chat-with-pdf\ --interactive`


For more information on the available APIs, please refer to the Azure OpenAI starter project.


## Sources & further resources:
- https://microsoft.github.io/promptflow/how-to-guides/quick-start.html
- https://github.com/microsoft/promptflow/tree/main/examples