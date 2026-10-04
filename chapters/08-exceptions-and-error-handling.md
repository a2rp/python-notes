# 8. Exceptions and error handling

[Back to notes index](../README.md)

| [Previous: Modules, imports, and packages](07-modules-imports-and-packages.md) | [Notes index](../README.md) | [Next: Files, paths, JSON, and CSV](09-files-paths-json-and-csv.md) |
|:--|:--:|--:|

This chapter explains exception types, raising errors, handling failures, and cleanup.

## In this chapter

- try, except, else, and finally
- Raising built-in and custom exceptions
- Exception chaining
- Context managers and cleanup
- Eight review questions

## Catch only failures you can handle

An exception interrupts normal execution and carries a type and message. Catch a specific exception when the program has a useful recovery action.

~~~python
raw_count = "12"

try:
    count = int(raw_count)
except ValueError:
    count = 0
else:
    print(f"Loaded {count} items")

print(count)
~~~

The except block runs only when the matching exception occurs. The else block runs only when the try block finishes without an exception. Put narrower exception types before their broader parent types.

Do not use a bare except to hide programming errors. Catching BaseException also catches signals such as KeyboardInterrupt and should almost never be used for ordinary recovery.

## Raise clear errors

Use a built-in exception type that describes the invalid operation. Define a custom exception when callers need to distinguish one domain failure:

~~~python
class TaskNotFoundError(LookupError):
    pass


def get_task(tasks, task_id):
    try:
        return tasks[task_id]
    except KeyError as error:
        raise TaskNotFoundError(f"Task {task_id} was not found") from error
~~~

raise ... from keeps the original exception as the cause. This gives a useful traceback without forcing a caller to understand the internal dictionary lookup.

Validate external inputs explicitly. assert is for developer assumptions and may be removed when Python runs with optimization, so it is not input validation.

## Clean up reliably

finally runs whether the operation succeeds or raises. Prefer a context manager when a resource supports one, because it handles cleanup at the correct boundary:

~~~python
from pathlib import Path

path = Path("tasks.txt")
with path.open("r", encoding="utf-8") as file:
    contents = file.read()
~~~

The file closes when the with block exits, including when reading raises an exception. Use context managers for files, locks, and other resources with a defined acquire/release lifecycle.

If cleanup itself can fail, decide how to preserve the original error. Do not silently discard either failure.

## Review questions

1. When should a function catch an exception?
2. What does the try block's else clause mean?
3. Why should exception handlers catch specific types?
4. Why is a bare except usually a poor choice?
5. When should a custom exception be defined?
6. What does raise NewError(...) from error preserve?
7. Why is assert not appropriate for validating user input?
8. How does a context manager help clean up a file?

## References

- [Python: Exceptions in the execution model](https://docs.python.org/3.14/reference/executionmodel.html#exceptions)
- [Python: The raise statement](https://docs.python.org/3.14/reference/simple_stmts.html#the-raise-statement)
- [Python: With statement](https://docs.python.org/3.14/reference/compound_stmts.html#the-with-statement)

---

| [Previous: Modules, imports, and packages](07-modules-imports-and-packages.md) | [Notes index](../README.md) | [Next: Files, paths, JSON, and CSV](09-files-paths-json-and-csv.md) |
|:--|:--:|--:|
