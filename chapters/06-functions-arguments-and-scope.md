# 6. Functions, arguments, and scope

[Back to notes index](../README.md)

| [Previous: Conditions, loops, and control flow](05-conditions-loops-and-control-flow.md) | [Notes index](../README.md) | [Next: Modules, imports, and packages](07-modules-imports-and-packages.md) |
|:--|:--:|--:|

This chapter covers function definitions, parameters, return values, closures, and local scope.

## In this chapter

- Positional and keyword arguments
- Defaults and mutable-default pitfalls
- *args and **kwargs
- Scope, closures, and simple decorators
- Eight review questions

## Define a function with a clear contract

def creates a function object. return sends a value to the caller; reaching the end without return produces None.

~~~python
def line_total(unit_price, quantity):
    return unit_price * quantity


total = line_total(19.50, 2)
~~~

Use positional arguments for the required sequence and keyword arguments when naming an option improves clarity:

~~~python
def greet(name, punctuation="!"):
    return f"Hello, {name}{punctuation}"


message = greet("Mira", punctuation=".")
~~~

A slash marks positional-only parameters. A bare asterisk marks keyword-only parameters:

~~~python
def create_user(name, /, *, active=True):
    return {"name": name, "active": active}


user = create_user("Dev", active=False)
~~~

This prevents callers from passing the first parameter by an unsupported keyword and makes the option explicit.

## Avoid mutable default arguments

Default values are evaluated once when the function is defined, not once per call. A mutable default is shared between calls:

~~~python
def add_tag(tag, tags=None):
    if tags is None:
        tags = []
    tags.append(tag)
    return tags
~~~

Using None creates a fresh list for each call. This pattern also distinguishes an omitted argument from a caller-supplied list.

## Accept a variable number of arguments

*args collects extra positional arguments into a tuple. **kwargs collects extra keyword arguments into a dictionary.

~~~python
def describe(first, *items, **options):
    return {
        "first": first,
        "items": items,
        "options": options,
    }


result = describe("start", "middle", "end", color="orange")
~~~

Use these forms for a real extension point or a wrapper. A long list of loosely defined options makes a function harder to call and maintain.

## Understand scope and closures

Python looks up local names, then enclosing function scopes, then module globals, then built-ins. Parameters and assignments inside a function are local unless declared otherwise.

~~~python
def make_counter():
    count = 0

    def next_value():
        nonlocal count
        count += 1
        return count

    return next_value


counter = make_counter()
print(counter())  # 1
print(counter())  # 2
~~~

The inner function closes over count, so that value remains available after make_counter returns. Prefer explicit inputs and outputs when a closure would hide too much mutable state.

## Wrap behavior with a decorator

A decorator receives a function and returns a replacement function. functools.wraps preserves useful metadata from the original function:

~~~python
from functools import wraps


def announce(function):
    @wraps(function)
    def wrapper(*args, **kwargs):
        print(f"Calling {function.__name__}")
        return function(*args, **kwargs)

    return wrapper
~~~

Decorators are useful for cross-cutting behavior such as logging or access checks. Keep them small because they add a layer between a function call and its implementation.

## Review questions

1. What value is returned when a function reaches its end without return?
2. When can a keyword argument make a call easier to read?
3. What do slash and bare asterisk mean in a parameter list?
4. When are default argument expressions evaluated?
5. Why is a mutable list usually a poor default argument?
6. What types collect extra positional and keyword arguments?
7. What does nonlocal let a nested function change?
8. What does functools.wraps preserve for a decorated function?

## References

- [Python: Function definitions](https://docs.python.org/3.14/reference/compound_stmts.html#function-definitions)
- [Python: Execution model and name resolution](https://docs.python.org/3.14/reference/executionmodel.html)
- [Python: functools.wraps](https://docs.python.org/3.14/library/functools.html#functools.wraps)

---

| [Previous: Conditions, loops, and control flow](05-conditions-loops-and-control-flow.md) | [Notes index](../README.md) | [Next: Modules, imports, and packages](07-modules-imports-and-packages.md) |
|:--|:--:|--:|
