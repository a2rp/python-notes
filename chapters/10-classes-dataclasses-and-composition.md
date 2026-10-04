# 10. Classes, dataclasses, and composition

[Back to notes index](../README.md)

| [Previous: Files, paths, JSON, and CSV](09-files-paths-json-and-csv.md) | [Notes index](../README.md) | [Next: Iterators and generators](11-iterators-and-generators.md) |
|:--|:--:|--:|

This chapter covers objects, instance state, methods, dataclasses, and composition.

## In this chapter

- Classes and instances
- Instance and class attributes
- Dataclasses and default factories
- Inheritance compared with composition
- Eight review questions

## Model an object with a class

A class defines behavior and the state each instance holds. Instance attributes belong to one object; class attributes are shared through the class unless an instance shadows them.

~~~python
class BankAccount:
    account_type = "checking"

    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("amount must be positive")
        self.balance += amount


account = BankAccount("Mira")
account.deposit(25)
~~~

The leading underscore in a name such as _balance is a convention that signals internal use. Python does not enforce private instance attributes. Use properties when reading or changing an attribute needs validation or a stable interface.

## Use dataclasses for data-focused objects

dataclass generates common methods such as initialization and representation. Use field(default_factory=...) for a fresh mutable value per instance:

~~~python
from dataclasses import dataclass, field


@dataclass
class Task:
    title: str
    tags: list[str] = field(default_factory=list)


first = Task("Read")
second = Task("Write")
first.tags.append("study")

print(first.tags)   # ["study"]
print(second.tags)  # []
~~~

A frozen dataclass prevents attribute reassignment through the normal interface. It is useful for value objects, but nested mutable values can still be changed:

~~~python
from dataclasses import dataclass


@dataclass(frozen=True)
class Point:
    x: float
    y: float
~~~

## Prefer composition for related behavior

Composition means one object contains or uses another object. It keeps responsibilities separate without building a deep inheritance tree:

~~~python
from dataclasses import dataclass


@dataclass(frozen=True)
class Address:
    city: str
    country: str


@dataclass
class Customer:
    name: str
    address: Address


customer = Customer("Mira", Address("Bengaluru", "India"))
print(customer.address.city)
~~~

Use inheritance when a subtype can stand in for its base type without surprising callers. Use super() to extend parent behavior and avoid depending on a specific parent implementation. Small, focused classes are easier to test than classes that own unrelated tasks.

## Review questions

1. What does a class define?
2. How do instance attributes differ from class attributes?
3. What does the leading underscore convention communicate?
4. Why use field(default_factory=list) in a dataclass?
5. What does frozen=True prevent?
6. Does a frozen dataclass make nested lists immutable?
7. What is composition?
8. When is inheritance appropriate?

## References

- [Python: Class definitions](https://docs.python.org/3.14/reference/compound_stmts.html#class-definitions)
- [Python: dataclasses](https://docs.python.org/3.14/library/dataclasses.html)

---

| [Previous: Files, paths, JSON, and CSV](09-files-paths-json-and-csv.md) | [Notes index](../README.md) | [Next: Iterators and generators](11-iterators-and-generators.md) |
|:--|:--:|--:|
