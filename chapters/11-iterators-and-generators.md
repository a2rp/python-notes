# 11. Iterators and generators

[Back to notes index](../README.md)

| [Previous: Classes, dataclasses, and composition](10-classes-dataclasses-and-composition.md) | [Notes index](../README.md) | [Next: Useful standard-library modules](12-standard-library-modules.md) |
|:--|:--:|--:|

This chapter explains iteration, iterables, iterator state, generators, and lazy processing.

## In this chapter

- Iterable and iterator protocols
- iter and next
- Generator functions and expressions
- Lazy pipelines and exhaustion
- Eight review questions

## Iterable and iterator

An iterable can produce an iterator. An iterator remembers its current position and returns the next value when next() is called. When no values remain, it raises StopIteration.

~~~python
values = [10, 20]
iterator = iter(values)

print(next(iterator))  # 10
print(next(iterator))  # 20
~~~

Most code should use for because the loop handles iterator exhaustion automatically:

~~~python
for value in values:
    print(value)
~~~

An iterator is usually exhausted after one pass. Call iter() on a reusable collection to get a new iterator.

## Yield values from a generator

A generator function uses yield to produce a value and pause. Its local state resumes when the next value is requested:

~~~python
def count_up_to(limit):
    current = 1
    while current <= limit:
        yield current
        current += 1


for number in count_up_to(3):
    print(number)
~~~

The function body does not run until iteration begins. This is useful for a large result or a stream that should be processed one value at a time.

yield from delegates iteration to another iterable:

~~~python
def all_names(groups):
    for group in groups:
        yield from group


print(list(all_names([["Mira", "Dev"], ["Ashish"]])))
~~~

## Use generator expressions for one-pass work

A generator expression has parentheses and computes values lazily. It can feed another function without building a temporary list:

~~~python
total_squares = sum(number * number for number in range(1, 6))
print(total_squares)
~~~

Use a list comprehension when the result must be reused or indexed. Use a generator when values can be consumed once. Do not create a generator when a small list is clearer.

## Review questions

1. What makes an object iterable?
2. What state does an iterator keep?
3. What exception signals that an iterator is exhausted?
4. What does a for loop handle for you?
5. When does a generator function begin executing?
6. What does yield from do?
7. When is a generator expression useful?
8. Why can a generator not be reused after it is exhausted?

## References

- [Python: Iterator types](https://docs.python.org/3.14/library/stdtypes.html#iterator-types)
- [Python: Yield expressions](https://docs.python.org/3.14/reference/expressions.html#yield-expressions)
- [Python: Generator expressions](https://docs.python.org/3.14/reference/expressions.html#generator-expressions)

---

| [Previous: Classes, dataclasses, and composition](10-classes-dataclasses-and-composition.md) | [Notes index](../README.md) | [Next: Useful standard-library modules](12-standard-library-modules.md) |
|:--|:--:|--:|
