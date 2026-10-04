# 1. Running Python and working with environments

[Back to notes index](../README.md)

| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: Names, values, and built-in types](02-names-values-and-types.md) |
|:--|:--:|--:|

This chapter introduces the Python interpreter, scripts, the interactive prompt, and isolated project environments.

## In this chapter

- Running Python interactively and from a file
- Reading tracebacks
- Creating a virtual environment
- Installing project packages
- Eight review questions

## Check the interpreter and run code

Python source is executed by an interpreter. Check which version the terminal will run:

~~~sh
python --version
python -c "print('Python is ready')"
~~~

On Windows, the Python launcher can select a specific installed version:

~~~powershell
py -3.14 --version
py -3.14 -c "print('Python is ready')"
~~~

The interactive prompt is useful for short experiments. Type an expression and Python evaluates it immediately. Leave the prompt with exit() or Ctrl+D on macOS and Linux; use Ctrl+Z followed by Enter in Windows terminals.

For saved work, put statements in a .py file and run it with the interpreter:

~~~python
name = "Mira"
print(f"Hello, {name}")
~~~

~~~sh
python hello.py
~~~

Use python -m pip instead of a bare pip command to make clear which interpreter receives the package.

## Isolate project packages

A virtual environment keeps one project's installed packages separate from other projects and the system interpreter. Create it from the project directory:

~~~sh
python -m venv .venv
~~~

Activate it in PowerShell:

~~~powershell
.venv\Scripts\Activate.ps1
~~~

Activate it in macOS or Linux:

~~~sh
source .venv/bin/activate
~~~

Then install a package into that environment:

~~~sh
python -m pip install requests
python -m pip show requests
~~~

Use python -m pip list to inspect installed packages. Leave the environment with deactivate. If activation is unavailable or inconvenient, call the environment's interpreter directly, such as .venv/bin/python or .venv\Scripts\python.exe.

Do not commit the .venv directory. Add it to .gitignore and record project dependencies in the format the project uses. A requirements file can capture an environment snapshot:

~~~sh
python -m pip freeze > requirements.txt
python -m pip install -r requirements.txt
~~~

For a library, declare direct dependencies and supported Python versions in project metadata rather than treating a full local environment snapshot as the library's dependency policy.

## Read a traceback

A traceback shows the call path that led to an exception. Read the final exception type and message first, then inspect the file and line locations above it. Fix the cause closest to the failing operation and rerun the command.

~~~python
values = [10, 20]
print(values[3])
~~~

The IndexError explains that the requested position is outside the list. The traceback line points to the operation that used it.

## Review questions

1. What does the Python interpreter do?
2. When is the interactive prompt useful?
3. How do you run a saved Python file?
4. Why use python -m pip instead of an ambiguous pip executable?
5. What problem does a virtual environment solve?
6. How do you activate a virtual environment on Windows and on macOS or Linux?
7. Why should the .venv directory stay out of version control?
8. Which part of a traceback should you read first?

## References

- [Python: Using Python](https://docs.python.org/3.14/using/index.html)
- [Python: Command-line and environment](https://docs.python.org/3.14/using/cmdline.html)
- [Python: venv](https://docs.python.org/3.14/library/venv.html)
- [Python: Installing Python modules](https://docs.python.org/3.14/installing/index.html)

---

| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: Names, values, and built-in types](02-names-values-and-types.md) |
|:--|:--:|--:|
