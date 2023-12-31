# Introduction
LangChain is a framework for developing applications powered by language models. It enables applications that:

1. Are context-aware: connect a language model to sources of context (prompt instructions, few shot examples, content to ground its response in, etc.)
2. Reason: rely on a language model to reason (about how to answer based on provided context, what actions to take, etc.)

The main value props of LangChain are:

* Components: abstractions for working with language models, along with a collection of implementations for each abstraction. Components are modular and easy-to-use, whether you are using the rest of the LangChain framework or not
* Off-the-shelf chains: a structured assembly of components for accomplishing specific higher-level tasks

Off-the-shelf chains make it easy to get started. For complex applications, components make it easy to customize existing chains and build new ones.


# **Langchain Setup and Usage**
<h2>Pip Commands</h2>

    pip install langchain

This will install the bare minimum requirements of LangChain. A lot of the value of LangChain comes when integrating it with various model providers, datastores, etc. By default, the dependencies needed to do that are NOT installed. However, there are two other ways to install LangChain that do bring in those dependencies.

To install modules needed for the common LLM providers, run:

    pip install langchain[llms]

To install all modules needed for all integrations, run:

    pip install langchain[all]

Note that if you are using zsh, you'll need to quote square brackets when passing them as an argument to a command, for example:

    pip install 'langchain[all]'

From source
If you want to install from source, you can do so by cloning the repo and be sure that the directory is PATH/TO/REPO/langchain/libs/langchain running:

    pip install -e .

<h5>Installation</h5>

**To install LangChain run:**

    pip install langchain



<h2>Conda Command</h2>

    conda install langchain -c conda-forge

This will install the bare minimum requirements of LangChain. A lot of the value of LangChain comes when integrating it with various model providers, datastores, etc. By default, the dependencies needed to do that are NOT installed. However, there are two other ways to install LangChain that do bring in those dependencies.

To install modules needed for the common LLM providers, run:

    pip install langchain[llms]

To install all modules needed for all integrations, run:

    pip install langchain[all]

Note that if you are using zsh, you'll need to quote square brackets when passing them as an argument to a command, for example:

    pip install 'langchain[all]'

From source
If you want to install from source, you can do so by cloning the repo and be sure that the directory is PATH/TO/REPO/langchain/libs/langchain running:

    pip install -e .

<h5>Installation</h5>

**To install LangChain run:**

    conda install langchain -c conda-forge
<hr>

<h2>Environment setup</h2>

Using LangChain will usually require integrations with one or more model providers, data stores, APIs, etc. For this example, we'll use OpenAI's model APIs.

First we'll need to install their Python package:

    pip install openai

Accessing the API requires an API key, which you can get by creating an account and heading here. Once we have a key we'll want to set it as an environment variable by running:

    export OPENAI_API_KEY="..."

If you'd prefer not to set an environment variable you can pass the key in directly via the openai_api_key named parameter when initiating the OpenAI LLM class:

    from langchain.llms import OpenAI    

    llm = OpenAI(openai_api_key="...")

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


    from langchain.llms import OpenAI    
    from langchain.chat_models import ChatOpenAI

    llm = OpenAI()
    chat_model = ChatOpenAI()

    llm.predict("hi!")
> >>> "Hi"

    chat_model.predict("hi!")

> >>> "Hi"




The OpenAI and ChatOpenAI objects are basically just configuration objects. You can initialize them with parameters like temperature and others, and pass them around.
<hr>

***Next, let's use the predict method to run over a string input.***

    text = "What would be a good company name for a company that makes colorful socks?"

    llm.predict(text)
> >>> Feetful of Fun

    chat_model.predict(text)
> >>> Socks O'Color

***Finally, let's use the predict_messages method to run over a list of messages.***

    from langchain.schema import HumanMessage

    text = "What would be a good company name for a company that makes colorful socks?"

    messages = [HumanMessage(content=text)]

    llm.predict_messages(messages)   
> >>> Feetful of Fun

    chat_model.predict_messages(messages)
> >>> Socks O'Color


**The predict() and predict_messages() methods in LangChain can take keyword arguments to override the settings that were configured when the object was created. This is useful for adjusting the temperature, which controls the creativity of the generated text.**

**For example, you could pass in temperature=0 to generate more predictable text, or temperature=1 to generate more creative text. You can also pass in other keyword arguments, such as length to control the length of the generated text.**




<h2>Prompt Templates</h2>


Most LLM applications use prompt templates to provide additional context to the LLM. Prompt templates can be used to generate a single string, or a list of messages.

***Advantages of using prompt templates:***

1. You can partial out variables, meaning you can format only some of the variables at a time.
2. You can compose prompt templates together, easily combining different templates into a single prompt.

***Example of using a prompt template to generate a single string:***

    from langchain.prompts import PromptTemplate

    prompt = PromptTemplate.from_template("What is a good name for a company that makes             {product}?")
    prompt.format(product="colorful socks")

Output:

> > "What is a good name for a company that makes colorful socks?"

***Example of using a prompt template to generate a list of messages:***


    from langchain.prompts.chat import ChatPromptTemplate

    template = "You are a helpful assistant that translates {input_language} to             
           {output_language}."
    human_template = "{text}"

    chat_prompt = ChatPromptTemplate.from_messages([
        ("system", template),
        ("human", human_template),
    ])

    chat_prompt.format_messages(input_language="English", output_language="French", text="I         love programming.")

Output:

>> [
SystemMessage(content="You are a helpful assistant that translates English to French.", additional_kwargs={}),
HumanMessage(content="I love programming.")
]

Conclusion:

Prompt templates are a powerful way to use LangChain to generate text. They allow you to provide additional context to the LLM, and to generate more complex and informative responses



<h2>Output parsers</h2>

***OutputParsers convert the raw output of an LLM into a format that can be used downstream. There are few main type of OutputParsers, including:***

* Convert text from LLM -> structured information (e.g. JSON)
* Convert a ChatMessage into just a string
* Convert the extra information returned from a call besides the message (like OpenAI function invocation) into a string.
<hr>

***we will write our own output parser - one that converts a comma separated list into a list.***

    from langchain.schema import BaseOutputParser`

    class CommaSeparatedListOutputParser(BaseOutputParser):

    """Parse the output of an LLM call to a comma-separated list."""


        def parse(self, text: str):
            """Parse the output of an LLM call."""
            return text.strip().split(", ")
 
    CommaSeparatedListOutputParser().parse("hi, bye")`

>>> ['hi', 'bye']



<h2>PromptTemplate + LLM + OutputParser</h2>

***We can now combine all these into one chain. This chain will take input variables, pass those to a prompt template to create a prompt, pass the prompt to a language model, and then pass the output through an (optional) output parser. This is a convenient way to bundle up a modular piece of logic. Let's see it in action!***

**Combined all code till now we study:**

    from langchain.chat_models import ChatOpenAI
    from langchain.prompts.chat import ChatPromptTemplate
    from langchain.schema import BaseOutputParser

    class CommaSeparatedListOutputParser(BaseOutputParser):
        """Parse the output of an LLM call to a comma-separated list."""


        def parse(self, text: str):
            """Parse the output of an LLM call."""
            return text.strip().split(", ")

    template = """You are a helpful assistant who generates comma separated lists.
        A user will pass in a category, and you should generate 5 objects in that category in         a comma separated list.
        ONLY return a comma separated list, and nothing more."""
    
    human_template = "{text}"

    chat_prompt = ChatPromptTemplate.from_messages([
        ("system", template),
        ("human", human_template),
    ])
    
    chain = chat_prompt | ChatOpenAI() | CommaSeparatedListOutputParser()
    
    chain.invoke({"text": "colors"})
***Output:***
> >> ['red', 'blue', 'green', 'yellow', 'orange']


# LangChain Expression Language (LCEL)


LangChain Expression Language (LCEL) is a way to write LangChain chains in a declarative manner. This has several benefits, including:

* Async, batch, and streaming support: Chains written in LCEL automatically have support for async, batch, and streaming operations. This makes it easy to prototype a chain in a Jupyter notebook using the sync interface, and then expose it as an async streaming interface.

* Fallbacks: LCEL makes it easy to attach fallbacks to any chain. This is important for handling the non-determinism of LLMs.
*Parallelism: LCEL automatically runs any components that can be run in parallel in parallel. This is important for LLM applications, which often involve long API calls.

* Seamless LangSmith tracing integration: LCEL automatically logs all steps of a chain to LangSmith for observability and debuggability.

Summary in simple terms:

***LCEL is a way to write LangChain chains that is easier to use and more efficient. It provides automatic support for async, batch, and streaming operations, fallbacks, parallelism, and LangSmith tracing. This makes it ideal for prototyping and deploying LLM applications.***


# InterFace

The Runnable protocol is a set of rules that LangChain components follow.This is a standard interface with a few different methods, which makes it easy to define custom chains as well as making it possible to invoke them in a standard way. This makes it easy to create new LangChain components and to use them together.

The three methods in the Runnable protocol are:

1. stream(): This method sends the response back to the user in chunks.
2. invoke(): This method runs the chain on a single input.
3. batch(): This method runs the chain on a list of inputs.


**stream():**

The stream() method in LangChain streams back chunks of the response. It takes an input as an argument and returns a generator object. The generator object can then be used to iterate over the response in chunks.

This can be useful for large responses, as it can help to reduce the load on the client and improve performance.

Here is an example of how to use the stream() method:


	import langchain

	# Create a LangChain chain.
	chain = langchain.Chain()
	chain.add_node(langchain.PromptNode(prompt="Write a novel about a cat."))
	chain.add_node(langchain.TextGenerationNode(model="gpt-neo"))

	# Invoke the chain and pass in the input "Write a novel about a cat.".
	output_generator = chain.stream({"text": "Write a novel about a cat."})

	# Iterate over the response in chunks and print each chunk to the console.
	for chunk in output_generator:
  	print(chunk)
This code will iterate over the response in chunks and print each chunk to the console. This can be useful for large responses, as it can help to reduce the load on the client and improve performance.


**invoke():**

The invoke() method in LangChain calls the chain on an input. It takes an input as an argument and returns the output of the chain.

This can be used to generate text, translate languages, write code, and perform other tasks.

Here is an example of how to use the invoke() method:


	import langchain

	# Create a LangChain chain.
	chain = langchain.Chain()
	chain.add_node(langchain.PromptNode(prompt="Write a poem about a cat."))
	chain.add_node(langchain.TextGenerationNode(model="gpt-neo"))

	# Invoke the chain and pass in the input "Write a poem about a cat.".
	output = chain.invoke({"text": "Write a poem about a cat."})

	# Print the output.
	print(output)
 
This code will print the following output:

>> Oh, cats are furry creatures,
>> With big eyes and tiny feet.
>> They love to play and chase the string,
>> And purr when they're asleep.

>> Cats are curious and independent,
>> But they also love to cuddle.
>> They're the perfect companions,
>> For people of all ages.





**batch():**

The batch() method in LangChain calls the chain on a list of inputs. It takes a list of inputs as an argument and returns a list of outputs.

This can be useful for tasks such as generating multiple poems or translating multiple sentences.

Here is an example of how to use the batch() method:


	import langchain

	# Create a LangChain chain.
	chain = langchain.Chain()
	chain.add_node(langchain.PromptNode(prompt="Write a poem about {}."))
	chain.add_node(langchain.TextGenerationNode(model="gpt-neo"))

	# Invoke the chain on a list of inputs.
	outputs = chain.batch([{"text": "cats"}, {"text": "dogs"}])

	# Print the outputs.
	for output in outputs:
  		print(output)

This code will print the following output:

>> Oh, cats are furry creatures,
>> With big eyes and tiny feet.
>> They love to play and chase the string,
>> And purr when they're asleep.

>> Cats are curious and independent,
>> But they also love to cuddle.
>> They're the perfect companions,
>> For people of all ages.

>> Dogs are loyal and loving creatures,
>> With wagging tails and wet noses.
>> They love to play fetch and go for walks,
>> And cuddle up with their owners at the end of the day.

>> Dogs are always happy to see their owners,
>> And they make great companions for people of all ages.


<hr>
<h3>Difference between stream(), invoke(), and batch()</h3>

1. The main difference between stream(), invoke(), and batch() is that stream() streams back chunks of the response, while invoke() and batch() return the entire output of the chain at once.

2. Another difference is that invoke() takes a single input as an argument, while batch() takes a list of inputs as an argument.

** Simpler explanation **

1. stream(): Returns a generator object that can be used to iterate over the response in chunks. This is useful for large responses, as it can help to reduce the load on the client and improve performance.
2. invoke(): Calls the chain on an input and returns the output of the chain. This can be used to generate text



**Using the Runnable protocol, you can create custom LangChain chains that can do anything you need them to do**
<hr>

These also have corresponding async methods:

* astream: stream back chunks of the response async
* ainvoke: call the chain on an input async
* abatch: call the chain on a list of inputs async
* astream_log: stream back intermediate steps as they happen, in addition to the final response



The asynchronous versions of the stream(), invoke(), and batch() methods are astream(), ainvoke(), abatch(), and astream_log(), respectively.

These methods work the same way as their synchronous counterparts, except that they return an asyncio.Future object instead of the result directly. This means that you can use them in asynchronous code without blocking the main thread.

Example

Here is an example of how to use the astream() method:

	import asyncio
	import langchain

	async def main():
  		# Create a LangChain chain.
  		chain = langchain.Chain()
  		chain.add_node(langchain.PromptNode(prompt="Write a novel about a cat."))
  		chain.add_node(langchain.TextGenerationNode(model="gpt-neo"))

  		# Invoke the chain and pass in the input "Write a novel about a cat.".
  		output_generator = chain.astream({"text": "Write a novel about a cat."})

  		# Iterate over the response in chunks and print each chunk to the console.
  		async for chunk in output_generator:
    		print(chunk)

	if __name__ == "__main__":
  	    asyncio.run(main())

This code will iterate over the response in chunks and print each chunk to the console. The main thread will not be blocked while the chain is running, so you can continue to do other work in the meantime.

***Difference between synchronous and asynchronous methods***

* The main difference between the synchronous and asynchronous methods is that the synchronous methods block the main thread until they have finished executing, while the asynchronous methods do not.

* This means that you can use the asynchronous methods in asynchronous code without blocking the main thread. This can be useful for improving the performance and responsiveness of your application.

**astream_log():**

The astream_log() method streams back intermediate steps as they happen, in addition to the final response. This can be useful for debugging or for monitoring the progress of the chain.

Example

Here is an example of how to use the astream_log() method:


	import asyncio
	import langchain

	async def main():
  		# Create a LangChain chain.
  		chain = langchain.Chain()
  		chain.add_node(langchain.PromptNode(prompt="Write a novel about a cat."))
  		chain.add_node(langchain.TextGenerationNode(model="gpt-neo"))

 		 # Invoke the chain and pass in the input "Write a novel about a cat.".
  		output_generator = chain.astream_log({"text": "Write a novel about a cat."})

  		# Iterate over the response and print each chunk to the console.
  		async for chunk in output_generator:
    			print(chunk)

	if __name__ == "__main__":
 		 asyncio.run(main())

This code will print each chunk of the response to the console, as well as the intermediate steps. This can be useful for debugging or for monitoring the progress of the chain.

Conclusion

* The asynchronous versions of the stream(), invoke(), and batch() methods are useful for writing asynchronous code with LangChain. They allow you to call chains and receive the response without blocking the main thread.

* The astream_log() method is useful for debugging or for monitoring the progress of a chain. It streams back intermediate steps as they happen, in addition to the final response.



<hr>

The type of the input varies by component:
<table>
    <tr>
        <th>Component</th>
        <th>Input Type</th>
    </tr>
    <tr>
        <td>Prompt</td>
        <td>Dictionary</td>
    </tr>
	<td>Retriever</td>
	<td>Single string</td>
    <tr>
       <td>LLM, ChatModel</td>
	<td>Single string, list of chat messages or a PromptValue</td>
    </tr>
    <tr>
	<td>Tool</td>
	<td>Single string, or dictionary, depending on the tool</td>
    </tr>
    <tr>
	<td>OutputParser</td>
	<td>The output of an LLM or ChatModel</td>
    </tr>
    
</table>


	
	
	
