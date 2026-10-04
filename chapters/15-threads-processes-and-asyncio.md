# 15. Threads, processes, and asyncio

[Back to notes index](../README.md)

| [Previous: Testing, debugging, and logging](14-testing-debugging-and-logging.md) | [Notes index](../README.md) | [Next: Capstone: command-line task tracker](16-capstone-command-line-task-tracker.md) |
|:--|:--:|--:|

This chapter compares concurrency tools and helps choose one based on the kind of work.

## In this chapter

- Blocking and non-blocking work
- Threads and shared state
- Processes and CPU-bound work
- asyncio tasks and cancellation
- Eight review questions

## Choose a concurrency model

Concurrency lets a program make progress on more than one task during the same period. Pick a tool based on the work:

- Threads are useful when tasks spend time waiting on blocking I/O.
- Processes can run CPU-heavy Python work in separate processes and provide stronger isolation.
- asyncio runs many cooperative I/O tasks on an event loop when the libraries they use support async operations.

Concurrency adds coordination and failure handling. A simple sequential program is often easier to understand and fast enough.

## Use a thread pool for blocking work

ThreadPoolExecutor runs blocking operations in worker threads and collects results:

~~~python
from concurrent.futures import ThreadPoolExecutor
from time import sleep


def read_remote_record(record_id):
    sleep(0.1)  # stands in for a blocking network request
    return {"id": record_id}


with ThreadPoolExecutor(max_workers=4) as executor:
    records = list(executor.map(read_remote_record, range(8)))
~~~

The context manager waits for its worker tasks before leaving. Avoid unsynchronized shared mutable state; pass input to workers and collect their returned values.

## Use processes for CPU-heavy work

ProcessPoolExecutor runs work in child processes. Keep worker functions at module level and guard process startup so the example also works with spawn-based platforms:

~~~python
from concurrent.futures import ProcessPoolExecutor


def square(number):
    return number * number


if __name__ == "__main__":
    with ProcessPoolExecutor() as executor:
        squares = list(executor.map(square, range(10)))
    print(squares)
~~~

Starting a process has overhead and arguments/results must be transferable between processes. For small tasks, the overhead can cost more than the work.

## Run cooperative I/O with asyncio

An async function pauses at await so the event loop can run another ready task. asyncio does not make blocking code non-blocking; use async-compatible libraries for network or file operations.

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

Cancellation is part of async control flow. Use try/finally around resources that need cleanup, and do not swallow asyncio.CancelledError when a task should stop.

Do not call time.sleep or a blocking network client inside an async task. Those operations block the event loop and delay every task that shares it.

## Review questions

1. What kind of work is a thread pool useful for?
2. When can a process pool help?
3. What are the costs of starting worker processes?
4. What kind of work fits asyncio?
5. Does asyncio make blocking functions non-blocking?
6. Why keep a process-pool worker function at module level?
7. What does await allow the event loop to do?
8. Why should cancellation cleanup be handled deliberately?

## References

- [Python: concurrent.futures](https://docs.python.org/3.14/library/concurrent.futures.html)
- [Python: asyncio](https://docs.python.org/3.14/library/asyncio.html)
- [Python: asyncio tasks](https://docs.python.org/3.14/library/asyncio-task.html)

---

| [Previous: Testing, debugging, and logging](14-testing-debugging-and-logging.md) | [Notes index](../README.md) | [Next: Capstone: command-line task tracker](16-capstone-command-line-task-tracker.md) |
|:--|:--:|--:|
