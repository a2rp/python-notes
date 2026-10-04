# 16. Capstone: command-line task tracker

[Back to notes index](../README.md)

| [Previous: Threads, processes, and asyncio](15-threads-processes-and-asyncio.md) | [Notes index](../README.md) | [Next: All code samples](98-all-code-samples.md) |
|:--|:--:|--:|

This chapter combines functions, dataclasses, JSON files, argument parsing, validation, and tests in a small command-line task tracker.

## In this chapter

- Define a task model
- Read and write JSON safely
- Add, list, and complete tasks
- Test core behavior
- Eight review questions

## Define the task model and file operations

The application stores a list of task records in JSON. The dataclass keeps the fields together, while the loading function checks that file data has the shape the program expects.

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

The temporary file is created in the destination directory, so os.replace can replace the target on the same filesystem. If the program stops before replacement, the previous JSON file remains intact and the temporary file is cleaned up.

This example assumes one person writes the file at a time. Two simultaneous processes can both choose the same next id and overwrite each other's changes. A database is a better fit when multiple writers or durable concurrent updates are required.

## Run the commands

The --data option selects the JSON file. Keep it before the subcommand:

~~~sh
python task_tracker.py --data tasks.json add "Read Python notes"
python task_tracker.py --data tasks.json list
python task_tracker.py --data tasks.json complete 1
~~~

list reads the file without rewriting it. add and complete write the updated task list only after validation succeeds.

## Test the core behavior

The model functions are separate from argparse and printing, so a test can check them with a temporary file:

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

Run the tests with python -m unittest discover -v from the directory containing both files. TemporaryDirectory removes its test data when the block ends.

## Review questions

1. Why use a dataclass for Task?
2. Why validate the shape of a parsed JSON file?
3. Why write to a temporary file before replacing tasks.json?
4. How does add_task choose the next task id?
5. What does load_tasks return when the data file does not exist?
6. What does argparse provide for this command-line program?
7. What happens when complete_task cannot find the requested id?
8. What limitation makes a JSON file unsuitable for concurrent writers?

## References

- [Python: argparse](https://docs.python.org/3.14/library/argparse.html)
- [Python: json](https://docs.python.org/3.14/library/json.html)
- [Python: tempfile](https://docs.python.org/3.14/library/tempfile.html)
- [Python: os.replace](https://docs.python.org/3.14/library/os.html#os.replace)
- [Python: unittest](https://docs.python.org/3.14/library/unittest.html)

---

| [Previous: Threads, processes, and asyncio](15-threads-processes-and-asyncio.md) | [Notes index](../README.md) | [Next: All code samples](98-all-code-samples.md) |
|:--|:--:|--:|
