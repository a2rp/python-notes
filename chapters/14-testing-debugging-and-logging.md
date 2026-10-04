# 14. Testing, debugging, and logging

[Back to notes index](../README.md)

| [Previous: Type hints and protocols](13-type-hints-and-protocols.md) | [Notes index](../README.md) | [Next: Threads, processes, and asyncio](15-threads-processes-and-asyncio.md) |
|:--|:--:|--:|

This chapter covers automated tests, assertions, debugging tools, and application logs.

## In this chapter

- unittest test cases and fixtures
- Testing errors and edge cases
- pdb and tracebacks
- Logging levels and useful context
- Eight review questions

## Test behavior with unittest

Keep core behavior in functions that can run without user input or external services. A test checks one expected behavior and reports a useful failure when it changes.

~~~python
# title_tools.py
def normalize_title(value):
    title = value.strip()
    if not title:
        raise ValueError("title must not be blank")
    return title
~~~

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

Run discovery from the project root:

~~~sh
python -m unittest discover -v
~~~

Test normal results, boundary values, and expected errors. Use setUp for small shared fixtures. Prefer a real simple object over a mock unless the test needs to isolate an external service or hard-to-trigger behavior.

## Debug a failure

Read the traceback from the final exception upward to find the failing operation and the calls that led to it. Add breakpoint() at a useful line to enter the debugger during local development. Remove temporary breakpoints before committing.

Use a small failing input to reproduce the issue. Check the values and types at the boundary where they first become incorrect.

## Record useful logs

The logging module supports levels and attaches context without building a separate print format for each message:

~~~python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(name)s %(message)s",
)
logger = logging.getLogger(__name__)

logger.info("Loaded %s tasks", 12)
~~~

Use DEBUG for details needed during diagnosis, INFO for meaningful progress, WARNING for recoverable problems, and ERROR for failures. In an exception handler, logger.exception records the traceback. Do not log passwords, access tokens, or sensitive personal data.

## Review questions

1. What should one unit test focus on?
2. How does unittest.assertRaises verify an expected failure?
3. Which command discovers and runs unittest tests?
4. Why should a function be separated from interactive input to make testing easier?
5. What does breakpoint() do?
6. Which logging method records an exception traceback?
7. Why can excessive mocking make tests less useful?
8. What kinds of values should not be written to logs?

## References

- [Python: unittest](https://docs.python.org/3.14/library/unittest.html)
- [Python: pdb and breakpoint](https://docs.python.org/3.14/library/pdb.html)
- [Python: logging](https://docs.python.org/3.14/library/logging.html)

---

| [Previous: Type hints and protocols](13-type-hints-and-protocols.md) | [Notes index](../README.md) | [Next: Threads, processes, and asyncio](15-threads-processes-and-asyncio.md) |
|:--|:--:|--:|
