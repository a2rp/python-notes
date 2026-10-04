# 12. Useful standard-library modules

[Back to notes index](../README.md)

| [Previous: Iterators and generators](11-iterators-and-generators.md) | [Notes index](../README.md) | [Next: Type hints and protocols](13-type-hints-and-protocols.md) |
|:--|:--:|--:|

This chapter highlights standard-library tools for dates, collections, paths, iteration, and structured text.

## In this chapter

- datetime and zoneinfo
- collections and itertools
- enum and functools
- logging, argparse, and subprocess basics
- Eight review questions

## Work with dates and time zones

Use aware datetimes for real instants and store them in UTC. Convert for display with zoneinfo when a named local time zone matters:

~~~python
from datetime import UTC, datetime
from zoneinfo import ZoneInfo

created_at = datetime.now(UTC)
local_time = created_at.astimezone(ZoneInfo("Asia/Kolkata"))

print(created_at.isoformat())
print(local_time.isoformat())
~~~

A naive datetime has no time-zone information. Do not silently treat one as UTC unless the source contract says that is correct. Daylight-saving transitions can make some local times ambiguous or nonexistent.

## Count and group with collections

Counter counts hashable values. defaultdict creates a default value when a key is first accessed:

~~~python
from collections import Counter, defaultdict

words = ["python", "notes", "python"]
counts = Counter(words)
print(counts["python"])  # 2

by_status = defaultdict(list)
by_status["open"].append("Read")
by_status["done"].append("Write")
~~~

Do not use defaultdict when a missing-key lookup should be an error; ordinary dictionary indexing makes that error visible.

## Combine iteration tools

itertools provides tools for composing iterators without building full intermediate collections:

~~~python
from itertools import chain, islice

first = ["a", "b"]
second = ["c", "d"]
combined = chain(first, second)
preview = list(islice(combined, 3))
print(preview)
~~~

islice consumes values from the iterator. It does not make a copy of the source collection.

## Run an external command safely

subprocess.run accepts an argument list. Avoid shell=True when values can come from an external source:

~~~python
import subprocess

result = subprocess.run(
    ["python", "--version"],
    check=True,
    capture_output=True,
    text=True,
)
print(result.stdout.strip() or result.stderr.strip())
~~~

check=True raises CalledProcessError when the command returns a nonzero exit code. Do not hide command failures if the next step depends on their output.

## Review questions

1. Why use an aware datetime for an event time?
2. What is datetime.now(UTC) returning?
3. How does ZoneInfo convert an instant for local display?
4. What does Counter count?
5. What happens when a missing key is read from defaultdict?
6. What does itertools.islice consume?
7. Why pass subprocess arguments as a list?
8. What does check=True do in subprocess.run?

## References

- [Python: datetime](https://docs.python.org/3.14/library/datetime.html)
- [Python: zoneinfo](https://docs.python.org/3.14/library/zoneinfo.html)
- [Python: collections](https://docs.python.org/3.14/library/collections.html)
- [Python: itertools](https://docs.python.org/3.14/library/itertools.html)
- [Python: subprocess](https://docs.python.org/3.14/library/subprocess.html)

---

| [Previous: Iterators and generators](11-iterators-and-generators.md) | [Notes index](../README.md) | [Next: Type hints and protocols](13-type-hints-and-protocols.md) |
|:--|:--:|--:|
