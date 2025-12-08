**venv**

venv is a virtual environment that we create to install dependencies for a specific project.

It is a built-in Python tool made specifically to create isolated environments for Python projects.

Think of it like : **A seperate mini-Python world for one project**

why we use it:
- Keeps project libraries seperate
- Avoids version conflicts
- Keeps your system python clean

So when you create a venv -> everything installed inside it is only for that project.

What is a conflict or version conflict mean :

A version conflict happens when:

- Two projects need different versions of the same library, but your PC has only one version installed globally (if installed directly without using venv into the pc)

Every library has versions like : 1.0, 2.0, 2.5, 3.1

Now imagine this:

🔹 Project 1 needs:

> Django version 2.2

🔹 Project 2 needs:

> Fjango version 4.2

But your PC has only one Django installed globally at t time. 

So:
- If you install Django 4.2, Project 1 breaks
- If you downgrade to Django 2.2, Project 2 breaks

This problem is called version conflict.

With venv, each project gets its own private library room




