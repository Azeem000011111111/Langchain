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

<hr>



<h2>Building an application</h2>


LangChain is a framework for building language model applications. It provides modules that can be used as stand-alones or combined for more complex use cases. The most common chain contains three things:

1. LLM: The language model is the core reasoning engine.
2. Prompt Templates: This provides instructions to the language model.
3. Output Parsers: These translate the raw response from the LLM to a more workable format.

***This getting started guide will cover those three components and how to combine them. Understanding these concepts will set you up well for being able to use and customize LangChain applications.***

<hr>

<h2>LLM</h2>

LangChain has two types of language models:

1. LLMs: take a string as input and return a string
2. ChatModels: take a list of messages as input and return a message

A ChatMessage has two required components:

* content: the content of the message
* role: the role of the entity from which the ChatMessage is coming from

***This is useful for building chatbots and other conversational applications.***
<br>

LangChain provides several objects to easily distinguish between different roles in a conversation:

1. HumanMessage: A ChatMessage coming from a human/user.
2. AIMessage: A ChatMessage coming from an AI/assistant.
3. SystemMessage: A ChatMessage coming from the system.
4. FunctionMessage: A ChatMessage coming from a function call.

LangChain also provides a standard interface for both LLMs and ChatModels, with two methods:

* predict: Takes in a string, returns a string.
* predict_messages: Takes in a list of messages, returns a message.

***This makes it easy to build chatbots and other conversational applications using LangChain.***
<hr>

**let see an example with and LLM and Chat model:**


`from langchain.llms import OpenAI`
`from langchain.chat_models import ChatOpenAI`

`llm = OpenAI()`
`chat_model = ChatOpenAI()`

`llm.predict("hi!")`
> >>> "Hi"

`chat_model.predict("hi!")`

> >>> "Hi"




The OpenAI and ChatOpenAI objects are basically just configuration objects. You can initialize them with parameters like temperature and others, and pass them around.

***Next, let's use the predict method to run over a string input.***

`text = "What would be a good company name for a company that makes colorful socks?"`

`llm.predict(text)`
> >>> Feetful of Fun

`chat_model.predict(text)`
> >>> Socks O'Color

Finally, let's use the predict_messages method to run over a list of messages.

`from langchain.schema import HumanMessage`

`text = "What would be a good company name for a company that makes colorful socks?"`

`messages = [HumanMessage(content=text)]`

`llm.predict_messages(messages)`
> >>> Feetful of Fun

`chat_model.predict_messages(messages)`
> >>> Socks O'Color


**The predict() and predict_messages() methods in LangChain can take keyword arguments to override the settings that were configured when the object was created. This is useful for adjusting the temperature, which controls the creativity of the generated text.**

**For example, you could pass in temperature=0 to generate more predictable text, or temperature=1 to generate more creative text. You can also pass in other keyword arguments, such as length to control the length of the generated text.**

