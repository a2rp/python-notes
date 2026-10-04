# 4. Dictionaries, sets, and comprehensions

[Back to notes index](../README.md)

| [Previous: Strings and sequence types](03-strings-and-sequences.md) | [Notes index](../README.md) | [Next: Conditions, loops, and control flow](05-conditions-loops-and-control-flow.md) |
|:--|:--:|--:|

This chapter uses dictionaries and sets to model lookups and collections of unique values.

## In this chapter

- Dictionary creation and safe lookup
- Set membership and set operations
- Comprehensions
- Choosing the right collection
- Eight review questions

## Map keys to values with a dictionary

A dictionary maps hashable keys to values. It preserves insertion order, but code should use a dictionary because of its key lookup behavior, not because order was once undocumented.

~~~python
prices = {
    "MUG-01": 19.50,
    "BAG-02": 34.00,
}

print(prices["MUG-01"])
print(prices.get("LAMP-03"))            # None when the key is missing
print(prices.get("LAMP-03", 0.0))       # explicit fallback
~~~

Indexing with a missing key raises KeyError. Use get when absence is expected, or test membership when the missing case needs a separate action.

~~~python
if "MUG-01" in prices:
    print("Mug is listed")
~~~

Dictionary keys must be hashable and keep a stable hash while used as keys. Strings, numbers, and tuples of hashable values can be keys; lists and dictionaries cannot.

## Keep unique values with a set

A set stores unique hashable values and provides efficient membership checks. Its iteration order is not a presentation order.

~~~python
selected = {"MUG-01", "BAG-02", "MUG-01"}
print(selected)  # duplicate SKU appears once

available = {"MUG-01", "BAG-02", "LAMP-03"}
print(selected & available)  # intersection
print(available - selected)  # products not selected
print(selected | {"NOTE-04"})  # union
~~~

Use a list when position or repeated values matter. Use a set when uniqueness or membership is the main operation.

## Build collections with comprehensions

A comprehension creates a collection from an iterable and can include a condition:

~~~python
numbers = [1, 2, 3, 4, 5, 6]
even_squares = [number * number for number in numbers if number % 2 == 0]

prices = {"MUG-01": 19.50, "BAG-02": 34.00}
discounted = {sku: price * 0.9 for sku, price in prices.items()}
short_names = {sku for sku in prices if len(sku) <= 6}
~~~

Dictionary comprehensions overwrite earlier values if two inputs produce the same key. Set comprehensions remove duplicates.

Keep a comprehension simple enough to read at a glance. Use a normal loop when it needs multiple branches, error handling, logging, or side effects.

## Review questions

1. What does a dictionary store?
2. What happens when dictionary indexing uses a missing key?
3. When is dict.get useful?
4. Which kinds of values can be dictionary keys?
5. Does a set preserve an order suitable for display?
6. Which set operator computes an intersection?
7. What happens if two dictionary-comprehension inputs produce the same key?
8. When should a normal loop replace a comprehension?

## References

- [Python: Mapping types](https://docs.python.org/3.14/library/stdtypes.html#mapping-types-dict)
- [Python: Set types](https://docs.python.org/3.14/library/stdtypes.html#set-types-set-frozenset)
- [Python: Displays for lists, sets, and dictionaries](https://docs.python.org/3.14/reference/expressions.html#displays-for-lists-sets-and-dictionaries)

---

| [Previous: Strings and sequence types](03-strings-and-sequences.md) | [Notes index](../README.md) | [Next: Conditions, loops, and control flow](05-conditions-loops-and-control-flow.md) |
|:--|:--:|--:|
