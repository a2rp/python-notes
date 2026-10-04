# 3. Strings and sequence types

[Back to notes index](../README.md)

| [Previous: Names, values, and built-in types](02-names-values-and-types.md) | [Notes index](../README.md) | [Next: Dictionaries, sets, and comprehensions](04-dictionaries-sets-and-comprehensions.md) |
|:--|:--:|--:|

This chapter covers strings, bytes, lists, tuples, indexing, slicing, and useful sequence operations.

## In this chapter

- Unicode text and bytes
- Indexing and slicing
- List and tuple operations
- Sorting and copying sequences
- Eight review questions

## Text and bytes are different

str is Unicode text. bytes is a sequence of byte values. Convert between them with an explicit encoding, usually UTF-8:

~~~python
message = "café"
encoded = message.encode("utf-8")
decoded = encoded.decode("utf-8")

print(len(message))   # 4 Unicode code points
print(len(encoded))   # 5 bytes in UTF-8
print(decoded)        # café
~~~

The visible character count can differ from len because some displayed characters are made from multiple Unicode code points. Do not treat arbitrary bytes as text without knowing their encoding.

Strings are immutable. Methods such as replace return a new string:

~~~python
label = "  Python  "
clean = label.strip().lower()
print(label)  # original value stays unchanged
print(clean)  # python
~~~

F-strings insert expressions into readable output. For fixed decimal display, specify a format:

~~~python
price = 19.5
print(f"Price: {price:.2f}")
~~~

## Index and slice sequences

Lists and tuples are ordered sequences. Indexing starts at zero; a negative index counts from the end. A slice includes its start and excludes its stop.

~~~python
values = [10, 20, 30, 40, 50]

print(values[0])     # 10
print(values[-1])    # 50
print(values[1:4])   # [20, 30, 40]
print(values[::2])   # [10, 30, 50]
~~~

An out-of-range list index raises IndexError. A slice beyond the sequence ends safely at the available items.

## Change a list, preserve a tuple

Lists are mutable and suit collections that will be changed. append adds one object; extend adds each element from an iterable.

~~~python
items = ["book"]
items.append(["pen", "pad"])
print(items)  # ["book", ["pen", "pad"]]

items = ["book"]
items.extend(["pen", "pad"])
print(items)  # ["book", "pen", "pad"]
~~~

Tuples are immutable and are useful for fixed records or values that should not be reassigned by mutating the collection:

~~~python
point = (3, 7)
x, y = point
print(x, y)
~~~

Tuple immutability does not make nested mutable objects immutable.

## Sort and copy

sorted returns a new list. list.sort changes the original list and returns None. Provide a key function when sorting records by one field:

~~~python
names = ["mira", "Ashish", "dev"]
by_length = sorted(names, key=len)
case_insensitive = sorted(names, key=str.casefold)
~~~

A slice or list.copy creates a shallow copy. Nested objects remain shared, as shown in Chapter 2.

## Review questions

1. How are str and bytes different?
2. How do you encode text as UTF-8 bytes?
3. Why can len(text) differ from the number of visible characters?
4. Does str.replace change the original string?
5. Is a slice's stop position included?
6. What is the difference between list.append and list.extend?
7. How do sorted and list.sort differ?
8. What does a shallow copy of a nested list still share?

## References

- [Python: Text sequence type](https://docs.python.org/3.14/library/stdtypes.html#text-sequence-type-str)
- [Python: Sequence types](https://docs.python.org/3.14/library/stdtypes.html#sequence-types-list-tuple-range)
- [Python: Binary sequence types](https://docs.python.org/3.14/library/stdtypes.html#binary-sequence-types-bytes-bytearray-memoryview)
- [Python: Unicode HOWTO](https://docs.python.org/3.14/howto/unicode.html)

---

| [Previous: Names, values, and built-in types](02-names-values-and-types.md) | [Notes index](../README.md) | [Next: Dictionaries, sets, and comprehensions](04-dictionaries-sets-and-comprehensions.md) |
|:--|:--:|--:|
