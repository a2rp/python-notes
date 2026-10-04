# 13. Type hints and protocols

[Back to notes index](../README.md)

| [Previous: Useful standard-library modules](12-standard-library-modules.md) | [Notes index](../README.md) | [Next: Testing, debugging, and logging](14-testing-debugging-and-logging.md) |
|:--|:--:|--:|

This chapter uses annotations to communicate expected values and structural interfaces.

## In this chapter

- Built-in and union types
- Generic collections
- Typed functions and dataclasses
- Protocols and runtime behavior
- Eight review questions

## Annotate inputs and return values

Type hints describe intended types to readers and static analysis tools. Python does not automatically enforce them when a function runs.

~~~python
def format_name(first: str, last: str) -> str:
    return f"{first.strip()} {last.strip()}"
~~~

Use built-in collection types with their item types:

~~~python
def average(values: list[float]) -> float | None:
    if not values:
        return None
    return sum(values) / len(values)
~~~

The union type float | None means the function returns a number or no value. Callers should handle both cases.

## Describe structured values

TypedDict describes the expected keys and value types of a dictionary. It helps a type checker understand data from JSON, but the input still needs runtime validation:

~~~python
from typing import TypedDict


class TaskRecord(TypedDict):
    id: int
    title: str
    done: bool


def display_title(task: TaskRecord) -> str:
    return task["title"]
~~~

Use dataclasses when the program should create a runtime object with named attributes. Use TypedDict when the data naturally remains a dictionary.

## Use a protocol for behavior

A Protocol describes the operations an object must provide. A class can satisfy the protocol without inheriting from it:

~~~python
from typing import Protocol


class TextWriter(Protocol):
    def write(self, text: str) -> int:
        ...


def save_message(writer: TextWriter, message: str) -> None:
    writer.write(message)
~~~

Any object with a compatible write method can be passed to save_message. This structural approach keeps functions independent from a specific file or output class.

## Choose between Any and object

Any turns off many static checks for a value that flows through it. object is the safe type for an unknown value: code must narrow or check it before using type-specific operations.

~~~python
def show_value(value: object) -> str:
    if isinstance(value, (str, int, float)):
        return str(value)
    return "unsupported value"
~~~

Annotations do not replace validation at trust boundaries. A web request, file, or database row can still contain a value that does not match its annotation.

## Review questions

1. What do type hints communicate?
2. Does Python enforce annotations automatically at runtime?
3. What does str | None mean?
4. How do generic collection annotations describe item values?
5. What does TypedDict describe?
6. What is structural typing with a Protocol?
7. How does Any differ from object?
8. Why is validation still needed for data from a file or request?

## References

- [Python: typing](https://docs.python.org/3.14/library/typing.html)
- [Python: Protocols](https://docs.python.org/3.14/library/typing.html#typing.Protocol)
- [Python: Annotations and type hints](https://docs.python.org/3.14/glossary.html#term-annotation)

---

| [Previous: Useful standard-library modules](12-standard-library-modules.md) | [Notes index](../README.md) | [Next: Testing, debugging, and logging](14-testing-debugging-and-logging.md) |
|:--|:--:|--:|
