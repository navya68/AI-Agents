<img width="365" height="93" alt="image" src="https://github.com/user-attachments/assets/08b4bd09-7090-431e-9174-260e346bedf5" /># Building AI-Agent from scratch 

First, we should create a virtual environment using venv. This ensures that the required dependencies are installed only for the current project, avoiding conflicts with other projects.

To do that we should first create a virtual environment (I am using Vscode)

1. Create python virtual environment

```sh
python -m venv venv
```

2. After creating the virtual environment we should activate the virtual environemt

```sh
.\venv\Scripts\activate
```

⚠️ On Windows, you might get an error when activating the venv. Skip this step if there is no error.

3. Fixing Activation Errors (Windows PowerShell)
- VS Code uses PowerShell by default.
  
- On Windows, Powershell has a security feature called Execution Policy. Its purpose is to prevent unauthorized or potentially harmful scripts from running automatically. This is because scripts can run commands that might damage your system, steal data, or make unwanted changes.

- when you create a Python virtual environment (venv), activating it runs a script called Activate.ps1. Powershell sees this as a script that could potentially be unsafe.If your Execution Policy is set to Restricted (the default), PowerShell blocks all scripts, including the safe ones that Python generates for venv.

The error looks like:

```sh
PSSecurityException: running scripts is disabled on this system
```

This means: “PowerShell is refusing to run this script because my current security settings don’t allow any scripts to run.”

>It’s not an error with Python or your venv—it’s Windows protecting our system.

To fix this:

Open Powershell and run :

```sh
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```
- This temporarily allows scripts to run in the current session.

   
4. Activate the Virtual Environment Again
   
```sh
.\venv\Scripts\Activate.ps1
```

- After this, the venv folder is ready and your terminal will show the venv name.


5. Create requirements.txt

Create a file named requirements.txt in your project folder and add the dependencies:

```sh
langchain
wikipedia
langchain-community
langchain-openai
langchain-anthropic
python-dotenv
pydantic
google-generativeai
groq
```

These are the dependencies I will be using 

6. Now Install all the packages using pip

```sh
pip install -r .\requirements.txt
```

7. Upgrade pip (Optional)

If some dependencies fail to install, upgrade pip:
   
```sh
python -m pip install --upgrade pip
```

8. Confirmation

All dependencies will now be installed inside the venv folder, isolated from your system Python.

**Now we write the code**
1. Before that, let’s create a .env.example file to show required environment variables.

   - Create a file called:

     ```sh
     .env.example
     ```

   - Inside:

     ```sh
     GROQ_API_KEY=your_api_key_here
     ```
 ```sh
⚠️ Rename `.env.example` to `.env` locally and add your actual API key.
```
     
3. We should create main.py where we will be writing the main code

   ```python
   from dotenv import load_dotenv
   from pydantic import BaseModel
   from langchain_groq import ChatGroq
   load_dotenv()

   ##setup LLM
 
   llm = ChatGroq(model="llama-3.1-8b-instant")
   response = llm.invoke("what is your model name")
   print(response)
   ```

In my case I am using Groq as Groq provides a free tier with usage limits

- In the code I am using **load_dotenv** is a function this is used to load the environment variables that is .env file.
  - dotenv ->   Python package that reads .env files
  - load_dotenv → Function that loads environment variables from .env into the OS environment
  - Allows python to read API keys in .env
- **pydantic** -> This python package is used for Data Validation
- **BaseModel** -> This is a class used to define structured data
  # BaseModel will be used later for structured inputs
  - Helps define input/output in a clean format
- langchain_groq -> langchain groq integration
- ChatGroq -> class that connects to Groq LLMs
  - This is what actually talks to the AI Models

3. How does the object work why do we actually need it?

   - Python cannot directly talk the AI model that is the LLM. We need a bridge for the communication. That is where we use the object.

   - we are using Groq through Langchain. Langchain is just a python package(library). langchain_groq is a sub-package.
  
   - LangChain does not run models -it communicates with them via APIs.
  
   - Langchain contains python classes that knows how to talk to different LLMs.
  
   - In order to access those classes we need an object that is why we create an object and this object uses the methods in the class where the methods internally knows how to connect to the groq server.

  4. What is .env and how does it work

     - .env is used to store some private information like API Keys and all. Which can be loaded into the python file by load_dotenv() function.
    
     - The information in .env gets loaded into the OS environment variables whenever we run the file and when the session is completed the info gets erased.
    
  5. The final folder structure look like this

     **project folder**
     
     ```
     project/
     │── main.py
     │── requirements.txt
     │── .env.example
     │── tools.py
     |── venv
     ```

     **Files that need not be uploaded to github**

     ```
     |── venv
     |── .env
     ```
     



