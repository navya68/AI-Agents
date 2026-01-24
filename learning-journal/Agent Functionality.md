# In the Previous md we discussed how to use LLM very simply 

**We just learned how to use LLM. Now let's learn how to add functionality to the Agent.**

1. First we are gonna setup the Prompt Template

   - Prompt Template is something that will kind of act as a template for any of the queries that we give to the LLM. So, that we can give it more information
     on what we actually want it to do.

   - To be more clear and simple "A prompt template defines the rules for how an answer should be given." This is fixed the question changes but the way the LLM explains
     or gives answer remains same.

   - Example:
     - **Without Prompt Template**
       
       User: 
       ```sh
       "What is AI?"
       ```
       Possible Answer:
       ```sh
       "AL is a branch of computer science that focuses on Creating systems
       capable of performing tasks that typically require human inteligence."
       ```
     

     - **With Prompt Template**
    
       Prompt Template:

       ```sh
       "Explain in simple words for a beginner. Use exactly 2 bullet points."
       ##This is just an example (this is not how a prompt template is written).
       ```
       User:
       ```sh
       "What is AI?"
       ```
       Output (behavior is fixed):
       ```sh
       - AI is about making computers act smart.
       - It helps machines learn and make decisions.
       ```

**LLM reads text but chat-based LLMs reads organized messages** -> That is when we need to send the user prompt/Input in a particualar format which is known as **Chat Format**

- The chat format contains structured messages.

- In LLM we use ChatPromptTemplate class for the chat format.

**One more thing to remember is structured input and prompt template are similar. The structured messages are converted to prompt template by from_messages() function.

- structured messages mean: Each message has ->

```sh
a role (system / human / placeholder)
a clearly defined purpose
optional variables to be filled at runtime
```

For example:

```sh
"role" : "System"
"content" : "You are a research assistant, help with the research topics"

"role" : "User"
"content" : ""Nuclear energy for data centers"
```

- This is the format we use define prompt template that is we use structured messages.

code:

```sh
prompt = ChatMessagePromptTemplate.from_messages(
    [
        (
            "system",
            """
            You are a research assistant that will help generate a research paper. Answer the user query
            and use necessary tools. Wrap the output in this format and provide no other text \n{format_instructions}
            """
        ),
        ("placeholder",{chat_history}""),
        ("human","{query}"),
        ("placeholder","{agent_scratchpad}"),
    ]
).partial(format_instructions = parser.get_format_instructions())
```

- In the above code we are creating an Obj for ChatMessagePromptTemplate class and using from_messages() function to convert the structured messages to prompt template.

- And in the above code "system", "human", and "placeholder" are predefined keywords that LangChain understands.

- System means we are sending it to the serever asking it to behave in a particular way.

- human -> User Input

- Placeholder is telling LangChain "I’ll insert messages here later"

- coming to the next important thing .partial() it is a function that is used to lock in values that do not change every time we run the program.

   - A prompt template can have variables

   - Some variables are dynamic (change at runtime)

   - Some are static (same every time)
 
   - .partial() is how we pre-fill static variables so we don’t have to pass them again and again.
 
   For example:

   ```sh
   template = "Hello {name}, follow {rules}"
   ```

  If rules never changes:

  ```sh
  template = template.partial(rules="Always respond in JSON")
  ```

  Now at runtime, you only pass:

  ```sh
  name="Navya"
  ```

- Now what is "parser.get_format_instructions()" -> It is a function that is used to convert the schema(the rulebook of how output should look) into normal text to pass it to the LangChain

- parser is already has the schema (parser is an object created to store the schema)

- get_format_instructions() -> converts the schema into human-readable instructions   

- write the control logic in Python
  
- LangChain converts parts of that logic into plain-text instructions for the LLM

**Now coming to output**

- LLM just return plain text and that needs to be in a particular format -> Structured output

- For this we use Pydantic package and PydanticOutputParser class

- The output rules for LLM can be in two formats **JSON/SCHEMAS**

- Schemas -> These are nothing but rulebooks (how the output format should be)

- Pydantic helps to define these schemas where we use BaseModel class

```sh
class ResearchResponse(BaseModel):
    topic:str
    summary:str
    sources:list[str]
    tools_used:list[str]
```

- Here ResearchResponse is our Schema

- And next we need to check if the output given by LLM follows the schema to do this we PydanticOutputParser class

```sh
parser = PydanticOutputParser(pydantic_object=ResearchResponse)
```
- parser is object of PydanticOutputParser class and pydantic_object is a parameter.


  
       
