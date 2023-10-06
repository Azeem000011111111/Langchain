# Lanchain Setup
<h1>Pip Commands</h1>

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



<h1>Conda Command</h1>

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



