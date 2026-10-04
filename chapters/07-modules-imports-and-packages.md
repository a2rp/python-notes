# 7. Modules, imports, and packages

[Back to notes index](../README.md)

| [Previous: Functions, arguments, and scope](06-functions-arguments-and-scope.md) | [Notes index](../README.md) | [Next: Exceptions and error handling](08-exceptions-and-error-handling.md) |
|:--|:--:|--:|

This chapter shows how Python code is organized into modules and packages.

## In this chapter

- Importing names and modules
- Module search paths
- Packages and __init__.py
- The main-module guard
- Eight review questions

## Put related code in modules

A module is a Python file. Keep reusable functions and constants in a module, then import the names that another file needs.

~~~text
studyapp/
    __init__.py
    pricing.py
    cli.py
~~~

~~~python
# studyapp/pricing.py
TAX_RATE = 0.08


def total_with_tax(amount):
    return amount * (1 + TAX_RATE)
~~~

~~~python
# studyapp/cli.py
from .pricing import total_with_tax


def main():
    print(total_with_tax(25))


if __name__ == "__main__":
    main()
~~~

Run a package module from its parent directory:

~~~sh
python -m studyapp.cli
~~~

The relative import works because Python knows cli.py is part of the studyapp package.

## Import deliberately

import module keeps names qualified, while from module import name brings a specific name into the current namespace:

~~~python
import math
from pathlib import Path

root = Path.cwd()
circle_area = math.pi * 2**2
~~~

Avoid from module import * because it hides where names came from and can overwrite existing names. Keep module imports near the top of a file and avoid expensive work or external side effects at import time.

Python searches for modules using its import path, including the current execution context, installed packages, and configured paths. A local file with the same name as a standard-library module can shadow that module, so avoid filenames such as json.py or random.py.

## Packages and entry points

A regular package can include __init__.py. It can be empty or expose a small intentional public interface. Keep the package import path stable so code can be run from the project root using python -m.

The name __name__ is "__main__" when a file is run as the program entry point. The guard lets a module provide reusable definitions without starting the program when imported.

Circular imports happen when modules depend on each other's names during import. Move shared values into a third module, or pass dependencies into functions, instead of relying on partially initialized modules.

## Review questions

1. What is a Python module?
2. What does a package group together?
3. Why is import * usually avoided?
4. What is the difference between importing a module and importing one name?
5. How does python -m run a package module?
6. What does the main-module guard prevent?
7. Why should module import time avoid side effects?
8. How can a project reduce circular imports?

## References

- [Python: The import system](https://docs.python.org/3.14/reference/import.html)
- [Python: Packages](https://docs.python.org/3.14/reference/import.html#packages)
- [Python: __main__](https://docs.python.org/3.14/library/__main__.html)

---

| [Previous: Functions, arguments, and scope](06-functions-arguments-and-scope.md) | [Notes index](../README.md) | [Next: Exceptions and error handling](08-exceptions-and-error-handling.md) |
|:--|:--:|--:|
