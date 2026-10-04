# All code samples

[Back to notes index](../README.md)

| [Previous: Capstone: command-line task tracker](16-capstone-command-line-task-tracker.md) | [Notes index](../README.md) | [Next: Complete Q&A](99-complete-q-and-a.md) |
|:--|:--:|--:|

This appendix collects every fenced code example from the 16 core chapters and keeps each sample beside a link to its notes.

## Chapter 1: Running Python and working with environments

[Open the chapter](01-running-python-and-environments.md)

### Sample 1

~~~sh
python --version
python -c "print('Python is ready')"
~~~

### Sample 2

~~~powershell
py -3.14 --version
py -3.14 -c "print('Python is ready')"
~~~

### Sample 3

~~~python
name = "Mira"
print(f"Hello, {name}")
~~~

### Sample 4

~~~sh
python hello.py
~~~

### Sample 5

~~~sh
python -m venv .venv
~~~

### Sample 6

~~~powershell
.venv\Scripts\Activate.ps1
~~~

### Sample 7

~~~sh
source .venv/bin/activate
~~~

### Sample 8

~~~sh
python -m pip install requests
python -m pip show requests
~~~

### Sample 9

~~~sh
python -m pip freeze > requirements.txt
python -m pip install -r requirements.txt
~~~

### Sample 10

~~~python
values = [10, 20]
print(values[3])
~~~

## Chapter 2: Names, values, and built-in types

[Open the chapter](02-names-values-and-types.md)

### Sample 1

~~~python
first = [1, 2]
second = first
second.append(3)

print(first)          # [1, 2, 3]
print(first is second)  # True
~~~

### Sample 2

~~~python
second = [9]
print(first)  # [1, 2, 3]
~~~

### Sample 3

~~~python
count = 12
ratio = 0.25
enabled = True
title = "Study notes"
payload = b"OK"
missing = None
~~~

### Sample 4

~~~python
result = None

if result is None:
    print("No result")
~~~

### Sample 5

~~~python
original = {"tags": ["python"]}
shallow = original.copy()
shallow["tags"].append("study")

print(original["tags"])  # ["python", "study"]
~~~

### Sample 6

~~~python
print(0.1 + 0.2 == 0.3)  # False
~~~

### Sample 7

~~~python
from decimal import Decimal

total = Decimal("0.10") + Decimal("0.20")
print(total)  # 0.30
~~~

## Chapter 3: Strings and sequence types

[Open the chapter](03-strings-and-sequences.md)

### Sample 1

~~~python
message = "café"
encoded = message.encode("utf-8")
decoded = encoded.decode("utf-8")

print(len(message))   # 4 Unicode code points
print(len(encoded))   # 5 bytes in UTF-8
print(decoded)        # café
~~~

### Sample 2

~~~python
label = "  Python  "
clean = label.strip().lower()
print(label)  # original value stays unchanged
print(clean)  # python
~~~

### Sample 3

~~~python
price = 19.5
print(f"Price: {price:.2f}")
~~~

### Sample 4

~~~python
values = [10, 20, 30, 40, 50]

print(values[0])     # 10
print(values[-1])    # 50
print(values[1:4])   # [20, 30, 40]
print(values[::2])   # [10, 30, 50]
~~~

### Sample 5

~~~python
items = ["book"]
items.append(["pen", "pad"])
print(items)  # ["book", ["pen", "pad"]]

items = ["book"]
items.extend(["pen", "pad"])
print(items)  # ["book", "pen", "pad"]
~~~

### Sample 6

~~~python
point = (3, 7)
x, y = point
print(x, y)
~~~

### Sample 7

~~~python
names = ["mira", "Ashish", "dev"]
by_length = sorted(names, key=len)
case_insensitive = sorted(names, key=str.casefold)
~~~

## Chapter 4: Dictionaries, sets, and comprehensions

[Open the chapter](04-dictionaries-sets-and-comprehensions.md)

### Sample 1

~~~python
prices = {
    "MUG-01": 19.50,
    "BAG-02": 34.00,
}

print(prices["MUG-01"])
print(prices.get("LAMP-03"))            # None when the key is missing
print(prices.get("LAMP-03", 0.0))       # explicit fallback
~~~

### Sample 2

~~~python
if "MUG-01" in prices:
    print("Mug is listed")
~~~

### Sample 3

~~~python
selected = {"MUG-01", "BAG-02", "MUG-01"}
print(selected)  # duplicate SKU appears once

available = {"MUG-01", "BAG-02", "LAMP-03"}
print(selected & available)  # intersection
print(available - selected)  # products not selected
print(selected | {"NOTE-04"})  # union
~~~

### Sample 4

~~~python
numbers = [1, 2, 3, 4, 5, 6]
even_squares = [number * number for number in numbers if number % 2 == 0]

prices = {"MUG-01": 19.50, "BAG-02": 34.00}
discounted = {sku: price * 0.9 for sku, price in prices.items()}
short_names = {sku for sku in prices if len(sku) <= 6}
~~~

## Chapter 5: Conditions, loops, and control flow

[Open the chapter](05-conditions-loops-and-control-flow.md)

### Sample 1

~~~python
tasks = []

if not tasks:
    print("There are no tasks")
~~~

### Sample 2

~~~python
name = supplied_name or "Guest"
print(name)
~~~

### Sample 3

~~~python
if score >= 90:
    grade = "A"
elif score >= 75:
    grade = "B"
else:
    grade = "Keep practicing"
~~~

### Sample 4

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

### Sample 5

~~~python
for index, task in enumerate(["read", "write"], start=1):
    print(index, task)
~~~

### Sample 6

~~~python
names = ["Mira", "Dev"]
scores = [92, 86]

for name, score in zip(names, scores, strict=True):
    print(name, score)
~~~

### Sample 7

~~~python
attempts = 0

while attempts < 3:
    attempts += 1
    print(f"Attempt {attempts}")
~~~

### Sample 8

~~~python
for value in [2, 4, 6]:
    if value % 2:
        print("Found an odd value")
        break
else:
    print("Every value was even")
~~~

## Chapter 6: Functions, arguments, and scope

[Open the chapter](06-functions-arguments-and-scope.md)

### Sample 1

~~~python
def line_total(unit_price, quantity):
    return unit_price * quantity


total = line_total(19.50, 2)
~~~

### Sample 2

~~~python
def greet(name, punctuation="!"):
    return f"Hello, {name}{punctuation}"


message = greet("Mira", punctuation=".")
~~~

### Sample 3

~~~python
def create_user(name, /, *, active=True):
    return {"name": name, "active": active}


user = create_user("Dev", active=False)
~~~

### Sample 4

~~~python
def add_tag(tag, tags=None):
    if tags is None:
        tags = []
    tags.append(tag)
    return tags
~~~

### Sample 5

~~~python
def describe(first, *items, **options):
    return {
        "first": first,
        "items": items,
        "options": options,
    }


result = describe("start", "middle", "end", color="orange")
~~~

### Sample 6

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

### Sample 7

~~~python
from functools import wraps


def announce(function):
    @wraps(function)
    def wrapper(*args, **kwargs):
        print(f"Calling {function.__name__}")
        return function(*args, **kwargs)

    return wrapper
~~~

## Chapter 7: Modules, imports, and packages

[Open the chapter](07-modules-imports-and-packages.md)

### Sample 1

~~~text
studyapp/
    __init__.py
    pricing.py
    cli.py
~~~

### Sample 2

~~~python
# studyapp/pricing.py
TAX_RATE = 0.08


def total_with_tax(amount):
    return amount * (1 + TAX_RATE)
~~~

### Sample 3

~~~python
# studyapp/cli.py
from .pricing import total_with_tax


def main():
    print(total_with_tax(25))


if __name__ == "__main__":
    main()
~~~

### Sample 4

~~~sh
python -m studyapp.cli
~~~

### Sample 5

~~~python
import math
from pathlib import Path

root = Path.cwd()
circle_area = math.pi * 2**2
~~~

## Chapter 8: Exceptions and error handling

[Open the chapter](08-exceptions-and-error-handling.md)

### Sample 1

~~~python
raw_count = "12"

try:
    count = int(raw_count)
except ValueError:
    count = 0
else:
    print(f"Loaded {count} items")

print(count)
~~~

### Sample 2

~~~python
class TaskNotFoundError(LookupError):
    pass


def get_task(tasks, task_id):
    try:
        return tasks[task_id]
    except KeyError as error:
        raise TaskNotFoundError(f"Task {task_id} was not found") from error
~~~

### Sample 3

~~~python
from pathlib import Path

path = Path("tasks.txt")
with path.open("r", encoding="utf-8") as file:
    contents = file.read()
~~~

## Chapter 9: Files, paths, JSON, and CSV

[Open the chapter](09-files-paths-json-and-csv.md)

### Sample 1

~~~python
from pathlib import Path

project_dir = Path.cwd()
data_dir = project_dir / "data"
data_dir.mkdir(exist_ok=True)

tasks_file = data_dir / "tasks.json"
print(tasks_file.exists())
~~~

### Sample 2

~~~python
from pathlib import Path

path = Path("notes.txt")
path.write_text("First line\nSecond line\n", encoding="utf-8")
contents = path.read_text(encoding="utf-8")
print(contents)
~~~

### Sample 3

~~~python
with Path("notes.txt").open("r", encoding="utf-8") as file:
    for line in file:
        print(line.rstrip())
~~~

### Sample 4

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

### Sample 5

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

## Chapter 10: Classes, dataclasses, and composition

[Open the chapter](10-classes-dataclasses-and-composition.md)

### Sample 1

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

### Sample 2

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

### Sample 3

~~~python
from dataclasses import dataclass


@dataclass(frozen=True)
class Point:
    x: float
    y: float
~~~

### Sample 4

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

## Chapter 11: Iterators and generators

[Open the chapter](11-iterators-and-generators.md)

### Sample 1

~~~python
values = [10, 20]
iterator = iter(values)

print(next(iterator))  # 10
print(next(iterator))  # 20
~~~

### Sample 2

~~~python
for value in values:
    print(value)
~~~

### Sample 3

~~~python
def count_up_to(limit):
    current = 1
    while current <= limit:
        yield current
        current += 1


for number in count_up_to(3):
    print(number)
~~~

### Sample 4

~~~python
def all_names(groups):
    for group in groups:
        yield from group


print(list(all_names([["Mira", "Dev"], ["Ashish"]])))
~~~

### Sample 5

~~~python
total_squares = sum(number * number for number in range(1, 6))
print(total_squares)
~~~

## Chapter 12: Useful standard-library modules

[Open the chapter](12-standard-library-modules.md)

### Sample 1

~~~python
from datetime import UTC, datetime
from zoneinfo import ZoneInfo

created_at = datetime.now(UTC)
local_time = created_at.astimezone(ZoneInfo("Asia/Kolkata"))

print(created_at.isoformat())
print(local_time.isoformat())
~~~

### Sample 2

~~~python
from collections import Counter, defaultdict

words = ["python", "notes", "python"]
counts = Counter(words)
print(counts["python"])  # 2

by_status = defaultdict(list)
by_status["open"].append("Read")
by_status["done"].append("Write")
~~~

### Sample 3

~~~python
from itertools import chain, islice

first = ["a", "b"]
second = ["c", "d"]
combined = chain(first, second)
preview = list(islice(combined, 3))
print(preview)
~~~

### Sample 4

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

## Chapter 13: Type hints and protocols

[Open the chapter](13-type-hints-and-protocols.md)

### Sample 1

~~~python
def format_name(first: str, last: str) -> str:
    return f"{first.strip()} {last.strip()}"
~~~

### Sample 2

~~~python
def average(values: list[float]) -> float | None:
    if not values:
        return None
    return sum(values) / len(values)
~~~

### Sample 3

~~~python
from typing import TypedDict


class TaskRecord(TypedDict):
    id: int
    title: str
    done: bool


def display_title(task: TaskRecord) -> str:
    return task["title"]
~~~

### Sample 4

~~~python
from typing import Protocol


class TextWriter(Protocol):
    def write(self, text: str) -> int:
        ...


def save_message(writer: TextWriter, message: str) -> None:
    writer.write(message)
~~~

### Sample 5

~~~python
def show_value(value: object) -> str:
    if isinstance(value, (str, int, float)):
        return str(value)
    return "unsupported value"
~~~

## Chapter 14: Testing, debugging, and logging

[Open the chapter](14-testing-debugging-and-logging.md)

### Sample 1

~~~python
# title_tools.py
def normalize_title(value):
    title = value.strip()
    if not title:
        raise ValueError("title must not be blank")
    return title
~~~

### Sample 2

~~~python
# test_title_tools.py
import unittest

from title_tools import normalize_title


class NormalizeTitleTests(unittest.TestCase):
    def test_strips_outer_whitespace(self):
        self.assertEqual(normalize_title("  Read  "), "Read")

    def test_rejects_blank_title(self):
        with self.assertRaises(ValueError):
            normalize_title("   ")


if __name__ == "__main__":
    unittest.main()
~~~

### Sample 3

~~~sh
python -m unittest discover -v
~~~

### Sample 4

~~~python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(name)s %(message)s",
)
logger = logging.getLogger(__name__)

logger.info("Loaded %s tasks", 12)
~~~

## Chapter 15: Threads, processes, and asyncio

[Open the chapter](15-threads-processes-and-asyncio.md)

### Sample 1

~~~python
from concurrent.futures import ThreadPoolExecutor
from time import sleep


def read_remote_record(record_id):
    sleep(0.1)  # stands in for a blocking network request
    return {"id": record_id}


with ThreadPoolExecutor(max_workers=4) as executor:
    records = list(executor.map(read_remote_record, range(8)))
~~~

### Sample 2

~~~python
from concurrent.futures import ProcessPoolExecutor


def square(number):
    return number * number


if __name__ == "__main__":
    with ProcessPoolExecutor() as executor:
        squares = list(executor.map(square, range(10)))
    print(squares)
~~~

### Sample 3

~~~python
import asyncio


async def load_record(record_id):
    await asyncio.sleep(0.1)  # stands in for an async network wait
    return {"id": record_id}


async def main():
    records = await asyncio.gather(
        load_record(1),
        load_record(2),
        load_record(3),
    )
    print(records)


asyncio.run(main())
~~~

## Chapter 16: Capstone: command-line task tracker

[Open the chapter](16-capstone-command-line-task-tracker.md)

### Sample 1

~~~python
# task_tracker.py
import argparse
import json
import os
import tempfile
from dataclasses import asdict, dataclass
from pathlib import Path


@dataclass
class Task:
    id: int
    title: str
    done: bool = False


def load_tasks(path):
    try:
        value = json.loads(path.read_text(encoding="utf-8"))
    except FileNotFoundError:
        return []

    if not isinstance(value, list):
        raise ValueError("task file must contain a JSON list")

    tasks = []
    for record in value:
        if not isinstance(record, dict):
            raise ValueError("each task must be a JSON object")
        if type(record.get("id")) is not int:
            raise ValueError("each task id must be an integer")
        if not isinstance(record.get("title"), str):
            raise ValueError("each task title must be text")
        if not isinstance(record.get("done"), bool):
            raise ValueError("each task done value must be true or false")
        tasks.append(Task(record["id"], record["title"], record["done"]))
    return tasks


def save_tasks(path, tasks):
    path.parent.mkdir(parents=True, exist_ok=True)
    temporary_path = None

    try:
        with tempfile.NamedTemporaryFile(
            mode="w",
            encoding="utf-8",
            dir=path.parent,
            prefix=path.name + ".",
            delete=False,
        ) as file:
            temporary_path = Path(file.name)
            json.dump(
                [asdict(task) for task in tasks],
                file,
                ensure_ascii=False,
                indent=2,
            )
            file.write("\n")

        os.replace(temporary_path, path)
    finally:
        if temporary_path is not None and temporary_path.exists():
            temporary_path.unlink()


def add_task(tasks, title):
    clean_title = title.strip()
    if not clean_title:
        raise ValueError("task title must not be blank")

    task_id = max((task.id for task in tasks), default=0) + 1
    task = Task(task_id, clean_title)
    tasks.append(task)
    return task


def complete_task(tasks, task_id):
    for task in tasks:
        if task.id == task_id:
            task.done = True
            return task
    return None


def build_parser():
    parser = argparse.ArgumentParser(description="Keep a small task list in a JSON file.")
    parser.add_argument("--data", type=Path, default=Path("tasks.json"))
    commands = parser.add_subparsers(dest="command", required=True)

    add_command = commands.add_parser("add", help="add a task")
    add_command.add_argument("title")
    commands.add_parser("list", help="show tasks")

    complete_command = commands.add_parser("complete", help="complete a task")
    complete_command.add_argument("task_id", type=int)
    return parser


def main():
    parser = build_parser()
    args = parser.parse_args()

    try:
        tasks = load_tasks(args.data)

        if args.command == "add":
            task = add_task(tasks, args.title)
            save_tasks(args.data, tasks)
            print(f"Added {task.id}: {task.title}")
        elif args.command == "list":
            if not tasks:
                print("No tasks")
            for task in tasks:
                marker = "x" if task.done else " "
                print(f"[{marker}] {task.id}: {task.title}")
        elif args.command == "complete":
            task = complete_task(tasks, args.task_id)
            if task is None:
                parser.error(f"task {args.task_id} was not found")
            save_tasks(args.data, tasks)
            print(f"Completed {task.id}: {task.title}")
    except (OSError, ValueError) as error:
        parser.error(str(error))


if __name__ == "__main__":
    main()
~~~

### Sample 2

~~~sh
python task_tracker.py --data tasks.json add "Read Python notes"
python task_tracker.py --data tasks.json list
python task_tracker.py --data tasks.json complete 1
~~~

### Sample 3

~~~python
# test_task_tracker.py
import unittest
from pathlib import Path
from tempfile import TemporaryDirectory

from task_tracker import Task, add_task, complete_task, load_tasks, save_tasks


class TaskTrackerTests(unittest.TestCase):
    def test_add_and_persist_task(self):
        with TemporaryDirectory() as directory:
            path = Path(directory) / "tasks.json"
            tasks = []

            task = add_task(tasks, "  Read  ")
            save_tasks(path, tasks)

            self.assertEqual(task, Task(1, "Read"))
            self.assertEqual(load_tasks(path), [Task(1, "Read")])

    def test_complete_existing_task(self):
        tasks = [Task(1, "Read")]

        completed = complete_task(tasks, 1)

        self.assertTrue(completed.done)

    def test_missing_task_returns_none(self):
        self.assertIsNone(complete_task([], 9))

    def test_blank_title_is_rejected(self):
        with self.assertRaises(ValueError):
            add_task([], "   ")


if __name__ == "__main__":
    unittest.main()
~~~

---

| [Previous: Capstone: command-line task tracker](16-capstone-command-line-task-tracker.md) | [Notes index](../README.md) | [Next: Complete Q&A](99-complete-q-and-a.md) |
|:--|:--:|--:|
