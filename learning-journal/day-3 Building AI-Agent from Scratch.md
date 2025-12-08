# Building AI-Agent from scratch 

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



