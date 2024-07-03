# Chat with PDF

Source: https://github.com/microsoft/promptflow/tree/main/examples/flows/chat/chat-with-pdf

This is a simple flow that allow you to ask questions about the content of a PDF file and get answers.
You can run the flow with a URL to a PDF file and question as argument.
Once it's launched it will download the PDF and build an index of the content. 
Then when you ask a question, it will look up the index to retrieve relevant content and post the question with the relevant content to OpenAI chat model (gpt-3.5-turbo or gpt4) to get an answer.

Learn more on corresponding [tutorials](../../../tutorials/e2e-development/chat-with-pdf.md).


### CLI Example

#### Run flow

**Note**: this sample uses [predownloaded PDFs](./chat_with_pdf/.pdfs/) and [prebuilt FAISS Index](./chat_with_pdf/.index/) to speed up execution time.
You can remove the folders to start a fresh run.

```bash
# test with default input value in flow.dag.yaml
pf flow test --flow .

# test with flow inputs
pf flow test --flow . --inputs question="What is the name of the new language representation model introduced in the document?" pdf_url="https://arxiv.org/pdf/1810.04805.pdf"

# (Optional) create a random run name
run_name="web_classification_"$(openssl rand -hex 12)

# run with multiline data, --name is optional
pf run create --file batch_run.yaml --name $run_name

# visualize run output details
pf run visualize --name $run_name
```

#### Submit run to cloud

Assume we already have a connection named `open_ai_connection` in workspace.

```bash
# set default workspace
az account set -s <your_subscription_id>
az configure --defaults group=<your_resource_group_name> workspace=<your_workspace_name>
```

``` bash
# create run
pfazure run create --file batch_run.yaml --name $run_name
```

Note: Click portal_url of the run to view the final snapshot.
