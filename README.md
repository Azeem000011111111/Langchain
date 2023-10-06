# **Lanchain Setup**
<h2>Pip Commands</h2>

`pip install langchain`

This will install the bare minimum requirements of LangChain. A lot of the value of LangChain comes when integrating it with various model providers, datastores, etc. By default, the dependencies needed to do that are NOT installed. However, there are two other ways to install LangChain that do bring in those dependencies.

To install modules needed for the common LLM providers, run:

`pip install langchain[llms]`

To install all modules needed for all integrations, run:

`pip install langchain[all]`

Note that if you are using zsh, you'll need to quote square brackets when passing them as an argument to a command, for example:

`pip install 'langchain[all]'`

From source
If you want to install from source, you can do so by cloning the repo and be sure that the directory is PATH/TO/REPO/langchain/libs/langchain running:

`pip install -e .`

<h5>Installation</h5>

**To install LangChain run:**

`pip install langchain`



<h2>Conda Command</h2>

`conda install langchain -c conda-forge`

This will install the bare minimum requirements of LangChain. A lot of the value of LangChain comes when integrating it with various model providers, datastores, etc. By default, the dependencies needed to do that are NOT installed. However, there are two other ways to install LangChain that do bring in those dependencies.

To install modules needed for the common LLM providers, run:

`pip install langchain[llms]`

To install all modules needed for all integrations, run:

`pip install langchain[all]`

Note that if you are using zsh, you'll need to quote square brackets when passing them as an argument to a command, for example:

`pip install 'langchain[all]'`

From source
If you want to install from source, you can do so by cloning the repo and be sure that the directory is PATH/TO/REPO/langchain/libs/langchain running:

`pip install -e .`

<h5>Installation</h5>

**To install LangChain run:**

`conda install langchain -c conda-forge`
<hr>

<h2>Environment setup</h2>

Using LangChain will usually require integrations with one or more model providers, data stores, APIs, etc. For this example, we'll use OpenAI's model APIs.

First we'll need to install their Python package:

`pip install openai`

Accessing the API requires an API key, which you can get by creating an account and heading here. Once we have a key we'll want to set it as an environment variable by running:

`export OPENAI_API_KEY="..."`

If you'd prefer not to set an environment variable you can pass the key in directly via the openai_api_key named parameter when initiating the OpenAI LLM class:

`from langchain.llms import OpenAI`

`llm = OpenAI(openai_api_key="...")`


