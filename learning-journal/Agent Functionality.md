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
       
