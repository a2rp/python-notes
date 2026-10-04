# 9. Files, paths, JSON, and CSV

[Back to notes index](../README.md)

| [Previous: Exceptions and error handling](08-exceptions-and-error-handling.md) | [Notes index](../README.md) | [Next: Classes, dataclasses, and composition](10-classes-dataclasses-and-composition.md) |
|:--|:--:|--:|

This chapter reads and writes text files, paths, JSON documents, and CSV rows.

## In this chapter

- pathlib and file encodings
- Context managers and safe writes
- JSON serialization
- CSV readers and writers
- Eight review questions

## Work with paths

Path represents a filesystem path using operations that work across operating systems. Use the / operator to join path parts:

~~~python
from pathlib import Path

project_dir = Path.cwd()
data_dir = project_dir / "data"
data_dir.mkdir(exist_ok=True)

tasks_file = data_dir / "tasks.json"
print(tasks_file.exists())
~~~

Do not build paths by joining strings with a slash. A path can be relative or absolute; resolve it when an absolute location is needed. Treat paths from users as untrusted input and restrict them to the directories the program is allowed to access.

## Read and write text

Specify the text encoding so behavior does not depend on the operating system's default:

~~~python
from pathlib import Path

path = Path("notes.txt")
path.write_text("First line\nSecond line\n", encoding="utf-8")
contents = path.read_text(encoding="utf-8")
print(contents)
~~~

For large files or streaming work, open the file and process it a line at a time:

~~~python
with Path("notes.txt").open("r", encoding="utf-8") as file:
    for line in file:
        print(line.rstrip())
~~~

## Store structured data with JSON

JSON supports objects, arrays, strings, numbers, booleans, and null. Python maps those values to dictionaries, lists, strings, numbers, bool, and None.

~~~python
import json
from pathlib import Path

tasks = [{"id": 1, "title": "Read", "done": False}]
path = Path("tasks.json")

path.write_text(
    json.dumps(tasks, indent=2, ensure_ascii=False) + "\n",
    encoding="utf-8",
)

loaded = json.loads(path.read_text(encoding="utf-8"))
print(loaded[0]["title"])
~~~

json.loads validates JSON syntax, not the application's data model. Check required keys and value types before using data from a file or an external service. JSON does not directly represent values such as datetime or Decimal without a deliberate conversion.

## Read and write CSV rows

Use newline="" when opening CSV files so the csv module handles newline rules consistently. DictReader and DictWriter map each row to named fields:

~~~python
import csv
from pathlib import Path

path = Path("products.csv")
rows = [
    {"sku": "MUG-01", "name": "Travel mug", "price": "19.50"},
    {"sku": "BAG-02", "name": "Canvas bag", "price": "34.00"},
]

with path.open("w", newline="", encoding="utf-8") as file:
    writer = csv.DictWriter(file, fieldnames=["sku", "name", "price"])
    writer.writeheader()
    writer.writerows(rows)

with path.open("r", newline="", encoding="utf-8") as file:
    for row in csv.DictReader(file):
        print(row["sku"], row["price"])
~~~

CSV values are text. Convert and validate numbers and dates after reading. Do not assume the incoming file has the expected headers or a valid row count.

## Review questions

1. Why use pathlib instead of joining path strings manually?
2. Why should text file encoding be explicit?
3. When is line-by-line reading useful?
4. Which Python values map naturally to JSON objects and arrays?
5. Does parsing JSON prove that the data matches the application's schema?
6. Why should user-provided file paths be restricted?
7. Why is newline="" used with the csv module?
8. What type do CSV readers return for cell values?

## References

- [Python: pathlib](https://docs.python.org/3.14/library/pathlib.html)
- [Python: json](https://docs.python.org/3.14/library/json.html)
- [Python: csv](https://docs.python.org/3.14/library/csv.html)

---

| [Previous: Exceptions and error handling](08-exceptions-and-error-handling.md) | [Notes index](../README.md) | [Next: Classes, dataclasses, and composition](10-classes-dataclasses-and-composition.md) |
|:--|:--:|--:|
