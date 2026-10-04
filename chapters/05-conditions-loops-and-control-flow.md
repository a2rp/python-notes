# 5. Conditions, loops, and control flow

[Back to notes index](../README.md)

| [Previous: Dictionaries, sets, and comprehensions](04-dictionaries-sets-and-comprehensions.md) | [Notes index](../README.md) | [Next: Functions, arguments, and scope](06-functions-arguments-and-scope.md) |
|:--|:--:|--:|

This chapter explains truth testing, conditional branches, loops, and control-flow statements.

## In this chapter

- Truthy and falsy values
- if, elif, and else
- for and while loops
- break, continue, and loop else
- Eight review questions

## Truth values and conditions

if checks truthiness. None, False, numeric zero, and empty collections are false in a condition. Most other objects are true.

~~~python
tasks = []

if not tasks:
    print("There are no tasks")
~~~

Use an explicit comparison when the business rule is about a specific value. For example, use count == 0 when zero has meaning. Use if count when any nonzero count is sufficient.

and and or short-circuit and return one of their operands, not necessarily a bool:

~~~python
name = supplied_name or "Guest"
print(name)
~~~

This is a useful fallback when an empty string should also mean "not supplied". Use an explicit None check when an empty string is a valid value.

## Branch with if and match

~~~python
if score >= 90:
    grade = "A"
elif score >= 75:
    grade = "B"
else:
    grade = "Keep practicing"
~~~

For simple structural choices, match can make the alternatives clear:

~~~python
command = ("complete", 42)

match command:
    case ("complete", task_id):
        print(f"Complete task {task_id}")
    case ("list",):
        print("List tasks")
    case _:
        print("Unknown command")
~~~

The order matters: the first matching case runs. A wildcard case catches anything not matched above it.

## Iterate over values

for loops consume any iterable. range(stop) starts at zero and excludes stop. enumerate gives an index and value without maintaining a counter manually.

~~~python
for index, task in enumerate(["read", "write"], start=1):
    print(index, task)
~~~

zip combines iterables pairwise. strict=True raises ValueError if their lengths differ, which is useful when unequal lengths indicate a bug:

~~~python
names = ["Mira", "Dev"]
scores = [92, 86]

for name, score in zip(names, scores, strict=True):
    print(name, score)
~~~

## Repeat with while and control loop flow

Use while when the number of iterations depends on a condition. Make sure each path either updates the condition or exits:

~~~python
attempts = 0

while attempts < 3:
    attempts += 1
    print(f"Attempt {attempts}")
~~~

break exits the nearest loop. continue skips to its next iteration. A loop's else block runs only when the loop finishes without break:

~~~python
for value in [2, 4, 6]:
    if value % 2:
        print("Found an odd value")
        break
else:
    print("Every value was even")
~~~

The else clause belongs to the loop, not to an if statement. Use it only when the no-break case makes the code clearer.

## Review questions

1. Which common values are false in a condition?
2. When should an explicit comparison be used instead of truthiness?
3. Do and and or always return a bool?
4. What does range(stop) include?
5. Why use enumerate in a loop?
6. What does zip(..., strict=True) do when lengths differ?
7. What is the difference between break and continue?
8. When does a loop's else block execute?

## References

- [Python: Compound statements](https://docs.python.org/3.14/reference/compound_stmts.html)
- [Python: Boolean operations](https://docs.python.org/3.14/reference/expressions.html#boolean-operations)
- [Python: Built-in functions](https://docs.python.org/3.14/library/functions.html)

---

| [Previous: Dictionaries, sets, and comprehensions](04-dictionaries-sets-and-comprehensions.md) | [Notes index](../README.md) | [Next: Functions, arguments, and scope](06-functions-arguments-and-scope.md) |
|:--|:--:|--:|
