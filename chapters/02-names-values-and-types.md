# 2. Names, values, and built-in types

[Back to notes index](../README.md)

| [Previous: Running Python and working with environments](01-running-python-and-environments.md) | [Notes index](../README.md) | [Next: Strings and sequence types](03-strings-and-sequences.md) |
|:--|:--:|--:|

This chapter explains names, objects, basic values, identity, equality, and mutability.

## In this chapter

- Assignment and object references
- Numeric, boolean, string, and None values
- Mutable and immutable values
- Equality, identity, and copying
- Eight review questions

## Names refer to objects

Assignment binds a name to an object. It does not copy the object. Two names can refer to the same list:

~~~python
first = [1, 2]
second = first
second.append(3)

print(first)          # [1, 2, 3]
print(first is second)  # True
~~~

Rebinding one name does not rebind the other:

~~~python
second = [9]
print(first)  # [1, 2, 3]
~~~

Use clear names and remember that functions also receive references to objects. A function that mutates a list can change the same list the caller holds.

## Common built-in types

- int represents integers with arbitrary precision, limited by available memory.
- float represents binary floating-point values, so many decimal fractions are approximate.
- bool has the values True and False and is a subtype of int.
- str stores Unicode text. bytes stores byte values.
- None represents the absence of a value.
- list, dict, and set are mutable collections. tuple is immutable as a collection, though it can contain a mutable object.

~~~python
count = 12
ratio = 0.25
enabled = True
title = "Study notes"
payload = b"OK"
missing = None
~~~

Use type(value) while learning a value's exact type. In application code, prefer behavior and documented interfaces over repeated type checks.

## Equality and identity

== asks whether values are equal. is asks whether two names refer to the same object. Use identity checks for singleton sentinels such as None:

~~~python
result = None

if result is None:
    print("No result")
~~~

Do not use is to compare strings or numbers. Object reuse and interning are implementation details; equal values may or may not be the same object.

## Mutability and copying

Immutable values such as int, float, str, and tuple cannot be changed in place. A list or dictionary can be changed after creation.

~~~python
original = {"tags": ["python"]}
shallow = original.copy()
shallow["tags"].append("study")

print(original["tags"])  # ["python", "study"]
~~~

The dictionary copy is shallow: the outer dictionary is new but its nested list is shared. Use copy.deepcopy only when a recursive copy is actually needed and the contained objects support it.

## Exact decimal values

Binary floating-point is useful for scientific and general numeric work, but it cannot represent every decimal fraction exactly:

~~~python
print(0.1 + 0.2 == 0.3)  # False
~~~

Use math.isclose for approximate comparisons, or decimal.Decimal constructed from strings for exact decimal rules such as prices:

~~~python
from decimal import Decimal

total = Decimal("0.10") + Decimal("0.20")
print(total)  # 0.30
~~~

## Review questions

1. What does assignment do to a name and an object?
2. Why did appending through second also change first?
3. Which built-in collection types are mutable?
4. What does == compare?
5. When is is the appropriate comparison?
6. Why should is not be used to compare ordinary strings or numbers?
7. What does a shallow copy leave shared?
8. When is Decimal preferable to float?

## References

- [Python: Data model](https://docs.python.org/3.14/reference/datamodel.html)
- [Python: Built-in types](https://docs.python.org/3.14/library/stdtypes.html)
- [Python: decimal arithmetic](https://docs.python.org/3.14/library/decimal.html)
- [Python: math.isclose](https://docs.python.org/3.14/library/math.html#math.isclose)

---

| [Previous: Running Python and working with environments](01-running-python-and-environments.md) | [Notes index](../README.md) | [Next: Strings and sequence types](03-strings-and-sequences.md) |
|:--|:--:|--:|
