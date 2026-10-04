# Complete Q&A

[Back to notes index](../README.md)

| [Previous: All code samples](98-all-code-samples.md) | [Notes index](../README.md) | [Next: Notes index](../README.md) |
|:--|:--:|--:|

This appendix will gather eight answered review questions from each core chapter for a complete 128-question review set.

## Chapter 1: Running Python and working with environments

1. **What does the Python interpreter do?**  
   **Answer:** It reads Python code and executes its statements, reporting results or errors.
2. **When is the interactive prompt useful?**  
   **Answer:** It is useful for short experiments where a value or expression can be checked immediately.
3. **How do you run a saved Python file?**  
   **Answer:** Run the interpreter with the file name, such as python app.py.
4. **Why use python -m pip instead of an ambiguous pip executable?**  
   **Answer:** It runs pip through the selected interpreter, so packages install into that interpreter's environment.
5. **What problem does a virtual environment solve?**  
   **Answer:** It separates one project's packages from the system interpreter and other projects.
6. **How do you activate a virtual environment on Windows and on macOS or Linux?**  
   **Answer:** PowerShell uses .venv\Scripts\Activate.ps1. macOS and Linux shells use source .venv/bin/activate.
7. **Why should the .venv directory stay out of version control?**  
   **Answer:** It contains machine-specific installed files that can be recreated from project dependency information.
8. **Which part of a traceback should you read first?**  
   **Answer:** Read the final exception type and message, then follow the file and line details above it.

## Chapter 2: Names, values, and built-in types

1. **What does assignment do to a name and an object?**  
   **Answer:** Assignment binds a name to an object. It does not automatically make a copy.
2. **Why did appending through second also change first?**  
   **Answer:** Both names referred to the same mutable list, so changing it through either name changed that object.
3. **Which built-in collection types are mutable?**  
   **Answer:** list, dict, and set are mutable. tuple is immutable as a collection.
4. **What does == compare?**  
   **Answer:** It compares values for equality according to the objects' equality behavior.
5. **When is is the appropriate comparison?**  
   **Answer:** Use identity comparison for singleton values such as None or when object identity itself matters.
6. **Why should is not be used to compare ordinary strings or numbers?**  
   **Answer:** Equal values can be distinct objects, and object reuse is an implementation detail.
7. **What does a shallow copy leave shared?**  
   **Answer:** It creates a new outer container but keeps references to the same nested objects.
8. **When is Decimal preferable to float?**  
   **Answer:** Decimal is preferable when exact decimal arithmetic is required, such as for prices.

## Chapter 3: Strings and sequence types

1. **How are str and bytes different?**  
   **Answer:** str represents Unicode text. bytes represents byte values.
2. **How do you encode text as UTF-8 bytes?**  
   **Answer:** Call text.encode("utf-8") and decode the result with the matching encoding when it is read as text.
3. **Why can len(text) differ from the number of visible characters?**  
   **Answer:** len counts Unicode code points, while one visible character can be composed of multiple code points.
4. **Does str.replace change the original string?**  
   **Answer:** No. Strings are immutable, so replace returns a new string.
5. **Is a slice's stop position included?**  
   **Answer:** No. A slice includes its start position and excludes its stop position.
6. **What is the difference between list.append and list.extend?**  
   **Answer:** append adds one object. extend adds each item from an iterable.
7. **How do sorted and list.sort differ?**  
   **Answer:** sorted returns a new list. list.sort changes the list in place and returns None.
8. **What does a shallow copy of a nested list still share?**  
   **Answer:** It still shares the nested mutable lists or other mutable objects.

## Chapter 4: Dictionaries, sets, and comprehensions

1. **What does a dictionary store?**  
   **Answer:** A dictionary maps hashable keys to values.
2. **What happens when dictionary indexing uses a missing key?**  
   **Answer:** It raises KeyError.
3. **When is dict.get useful?**  
   **Answer:** It is useful when a missing key is expected and a default value or None is appropriate.
4. **Which kinds of values can be dictionary keys?**  
   **Answer:** Hashable values such as strings, numbers, and tuples containing only hashable values can be keys.
5. **Does a set preserve an order suitable for display?**  
   **Answer:** No. Set iteration order is not a presentation order.
6. **Which set operator computes an intersection?**  
   **Answer:** The ampersand operator computes the intersection.
7. **What happens if two dictionary-comprehension inputs produce the same key?**  
   **Answer:** The later value replaces the earlier value for that key.
8. **When should a normal loop replace a comprehension?**  
   **Answer:** Use a normal loop when the logic needs multiple branches, error handling, logging, or side effects.

## Chapter 5: Conditions, loops, and control flow

1. **Which common values are false in a condition?**  
   **Answer:** None, False, numeric zero, and empty collections are false.
2. **When should an explicit comparison be used instead of truthiness?**  
   **Answer:** Use an explicit comparison when the rule depends on a specific value, such as whether a count equals zero.
3. **Do and and or always return a bool?**  
   **Answer:** No. They short-circuit and return one of their operands.
4. **What does range(stop) include?**  
   **Answer:** It produces values starting at zero and stopping before stop.
5. **Why use enumerate in a loop?**  
   **Answer:** It provides an index and value together without a manually updated counter.
6. **What does zip(..., strict=True) do when lengths differ?**  
   **Answer:** It raises ValueError instead of silently dropping unmatched items.
7. **What is the difference between break and continue?**  
   **Answer:** break exits the nearest loop. continue skips to the next iteration.
8. **When does a loop's else block execute?**  
   **Answer:** It runs when the loop finishes without encountering break.

## Chapter 6: Functions, arguments, and scope

1. **What value is returned when a function reaches its end without return?**  
   **Answer:** It returns None.
2. **When can a keyword argument make a call easier to read?**  
   **Answer:** It helps when naming an option explains its meaning better than its position.
3. **What do slash and bare asterisk mean in a parameter list?**  
   **Answer:** Slash marks preceding parameters positional-only. A bare asterisk makes following parameters keyword-only.
4. **When are default argument expressions evaluated?**  
   **Answer:** They are evaluated once when the function is defined.
5. **Why is a mutable list usually a poor default argument?**  
   **Answer:** The same list would be shared by calls that omit the argument.
6. **What types collect extra positional and keyword arguments?**  
   **Answer:** *args collects a tuple of positional values, and **kwargs collects a dictionary of keyword values.
7. **What does nonlocal let a nested function change?**  
   **Answer:** It lets the nested function rebind a name from an enclosing function scope.
8. **What does functools.wraps preserve for a decorated function?**  
   **Answer:** It copies useful metadata such as the wrapped function's name and documentation.

## Chapter 7: Modules, imports, and packages

1. **What is a Python module?**  
   **Answer:** A module is a Python file whose definitions can be imported by other code.
2. **What does a package group together?**  
   **Answer:** A package groups related modules under a package namespace.
3. **Why is import * usually avoided?**  
   **Answer:** It hides where names came from and can overwrite names already in the module.
4. **What is the difference between importing a module and importing one name?**  
   **Answer:** Importing a module keeps names qualified by that module; importing one name binds it directly in the current namespace.
5. **How does python -m run a package module?**  
   **Answer:** It locates the module through the import system and runs it as the program entry point.
6. **What does the main-module guard prevent?**  
   **Answer:** It prevents entry-point code from running just because the module was imported.
7. **Why should module import time avoid side effects?**  
   **Answer:** Imports may happen as dependencies, so unexpected work or external changes make code harder to reuse and test.
8. **How can a project reduce circular imports?**  
   **Answer:** Move shared definitions to a third module or pass dependencies into functions instead of importing back and forth.

## Chapter 8: Exceptions and error handling

1. **When should a function catch an exception?**  
   **Answer:** It should catch an exception when it can recover or add useful context before raising or returning.
2. **What does the try block's else clause mean?**  
   **Answer:** The else block runs only when the try block finishes without an exception.
3. **Why should exception handlers catch specific types?**  
   **Answer:** Specific handlers avoid hiding unrelated programming errors and make recovery behavior clear.
4. **Why is a bare except usually a poor choice?**  
   **Answer:** It can catch unexpected errors and signals that the program should usually allow to propagate.
5. **When should a custom exception be defined?**  
   **Answer:** Define one when callers need to recognize and handle a domain-specific failure.
6. **What does raise NewError(...) from error preserve?**  
   **Answer:** It preserves the original exception as the explicit cause of the new exception.
7. **Why is assert not appropriate for validating user input?**  
   **Answer:** Assertions may be disabled during optimized execution and are intended for programmer assumptions.
8. **How does a context manager help clean up a file?**  
   **Answer:** It closes the file when the with block ends, even when an exception occurs.

## Chapter 9: Files, paths, JSON, and CSV

1. **Why use pathlib instead of joining path strings manually?**  
   **Answer:** pathlib provides path operations that handle platform-specific separators and path behavior.
2. **Why should text file encoding be explicit?**  
   **Answer:** It avoids depending on machine-specific defaults and reduces text corruption.
3. **When is line-by-line reading useful?**  
   **Answer:** It is useful for large files or streaming work that should not load the entire file into memory.
4. **Which Python values map naturally to JSON objects and arrays?**  
   **Answer:** Dictionaries map to JSON objects, and lists map to JSON arrays.
5. **Does parsing JSON prove that the data matches the application's schema?**  
   **Answer:** No. Parsing checks JSON syntax; the application must validate its expected keys and types.
6. **Why should user-provided file paths be restricted?**  
   **Answer:** Restricting paths prevents a program from reading or changing files outside its allowed area.
7. **Why is newline="" used with the csv module?**  
   **Answer:** It lets the csv module handle newline rules consistently, avoiding extra blank lines on some platforms.
8. **What type do CSV readers return for cell values?**  
   **Answer:** CSV readers return cell values as strings, which the application must convert and validate.

## Chapter 10: Classes, dataclasses, and composition

1. **What does a class define?**  
   **Answer:** It defines the behavior and instance structure used to create objects.
2. **How do instance attributes differ from class attributes?**  
   **Answer:** Instance attributes belong to one object. Class attributes are shared through the class unless shadowed.
3. **What does the leading underscore convention communicate?**  
   **Answer:** It signals that a name is intended for internal use.
4. **Why use field(default_factory=list) in a dataclass?**  
   **Answer:** It creates a separate list for each instance instead of sharing one mutable default.
5. **What does frozen=True prevent?**  
   **Answer:** It prevents ordinary reassignment of dataclass attributes after initialization.
6. **Does a frozen dataclass make nested lists immutable?**  
   **Answer:** No. The list can still be mutated even though the dataclass field cannot be reassigned.
7. **What is composition?**  
   **Answer:** Composition is a design where one object contains or uses another object to share responsibilities.
8. **When is inheritance appropriate?**  
   **Answer:** It is appropriate when a subtype can stand in for the base type without surprising callers.

## Chapter 11: Iterators and generators

1. **What makes an object iterable?**  
   **Answer:** It can provide an iterator, commonly through the __iter__ method.
2. **What state does an iterator keep?**  
   **Answer:** It keeps its current position or other state needed to produce the next value.
3. **What exception signals that an iterator is exhausted?**  
   **Answer:** StopIteration signals that there are no more values.
4. **What does a for loop handle for you?**  
   **Answer:** It obtains an iterator, requests values, and stops when iteration is exhausted.
5. **When does a generator function begin executing?**  
   **Answer:** It begins when code first requests a value from the generator.
6. **What does yield from do?**  
   **Answer:** It delegates producing values to another iterable or generator.
7. **When is a generator expression useful?**  
   **Answer:** It is useful for one-pass processing without building an intermediate list.
8. **Why can a generator not be reused after it is exhausted?**  
   **Answer:** Its iterator state has reached the end. Call the generator function again to create a new one.

## Chapter 12: Useful standard-library modules

1. **Why use an aware datetime for an event time?**  
   **Answer:** It identifies an instant with time-zone information and avoids ambiguity about the time zone.
2. **What is datetime.now(UTC) returning?**  
   **Answer:** It returns the current time as an aware datetime in UTC.
3. **How does ZoneInfo convert an instant for local display?**  
   **Answer:** astimezone applies the named zone's offset and daylight-saving rules to the same instant.
4. **What does Counter count?**  
   **Answer:** It counts occurrences of hashable values.
5. **What happens when a missing key is read from defaultdict?**  
   **Answer:** It creates a default value using the configured factory and stores it under that key.
6. **What does itertools.islice consume?**  
   **Answer:** It consumes only the requested number of items from its input iterator.
7. **Why pass subprocess arguments as a list?**  
   **Answer:** The executable and its arguments are passed separately without asking a shell to parse a combined command string.
8. **What does check=True do in subprocess.run?**  
   **Answer:** It raises CalledProcessError if the child process exits with a nonzero status.

## Chapter 13: Type hints and protocols

1. **What do type hints communicate?**  
   **Answer:** They communicate the intended value types to readers and static analysis tools.
2. **Does Python enforce annotations automatically at runtime?**  
   **Answer:** No. Annotations do not automatically validate values during function calls.
3. **What does str | None mean?**  
   **Answer:** It means the value can be a string or None.
4. **How do generic collection annotations describe item values?**  
   **Answer:** They specify the collection type and the type expected for its elements, such as list[str].
5. **What does TypedDict describe?**  
   **Answer:** It describes the expected keys and value types of a dictionary.
6. **What is structural typing with a Protocol?**  
   **Answer:** A value satisfies a protocol by providing compatible operations, even without inheriting from it.
7. **How does Any differ from object?**  
   **Answer:** Any disables many static checks for that value, while object requires type narrowing before specialized operations.
8. **Why is validation still needed for data from a file or request?**  
   **Answer:** External data can violate the annotation's expected shape because hints do not check it at runtime.

## Chapter 14: Testing, debugging, and logging

1. **What should one unit test focus on?**  
   **Answer:** It should check one behavior or rule with a clear expected result.
2. **How does unittest.assertRaises verify an expected failure?**  
   **Answer:** It passes only when the code inside its context manager raises the specified exception.
3. **Which command discovers and runs unittest tests?**  
   **Answer:** python -m unittest discover -v runs discovery with verbose output.
4. **Why should a function be separated from interactive input to make testing easier?**  
   **Answer:** A test can call the function directly without simulating a terminal session.
5. **What does breakpoint() do?**  
   **Answer:** It starts the configured debugger at that point in the running program.
6. **Which logging method records an exception traceback?**  
   **Answer:** logger.exception records a message and the active exception traceback.
7. **Why can excessive mocking make tests less useful?**  
   **Answer:** A test can end up checking the mock setup instead of the real behavior and interactions.
8. **What kinds of values should not be written to logs?**  
   **Answer:** Passwords, access tokens, and sensitive personal data should not be logged.

## Chapter 15: Threads, processes, and asyncio

1. **What kind of work is a thread pool useful for?**  
   **Answer:** It is useful for tasks that spend time waiting on blocking I/O.
2. **When can a process pool help?**  
   **Answer:** It can help with CPU-heavy work that benefits from separate processes.
3. **What are the costs of starting worker processes?**  
   **Answer:** Processes use memory and startup time, and their inputs and outputs must be transferred.
4. **What kind of work fits asyncio?**  
   **Answer:** Many I/O-bound tasks fit when their libraries provide non-blocking async operations.
5. **Does asyncio make blocking functions non-blocking?**  
   **Answer:** No. Blocking work still blocks the event loop unless it is moved to an appropriate worker.
6. **Why keep a process-pool worker function at module level?**  
   **Answer:** It makes the function importable and serializable by the child process on spawn-based platforms.
7. **What does await allow the event loop to do?**  
   **Answer:** It pauses the current coroutine so another ready task can run while this operation waits.
8. **Why should cancellation cleanup be handled deliberately?**  
   **Answer:** A cancelled task may need to release resources or leave shared state consistent before it stops.

## Chapter 16: Capstone command-line task tracker

1. **Why use a dataclass for Task?**  
   **Answer:** It gives each task named fields and generates common methods such as initialization and equality.
2. **Why validate the shape of a parsed JSON file?**  
   **Answer:** Valid JSON syntax does not guarantee the keys and values meet the task tracker's requirements.
3. **Why write to a temporary file before replacing tasks.json?**  
   **Answer:** It avoids exposing a partially written target file if serialization or writing fails.
4. **How does add_task choose the next task id?**  
   **Answer:** It finds the largest current id, defaults to zero when the list is empty, and adds one.
5. **What does load_tasks return when the data file does not exist?**  
   **Answer:** It returns an empty list so the tracker can start with no tasks.
6. **What does argparse provide for this command-line program?**  
   **Answer:** It parses options and subcommands, validates argument forms, and generates usage help.
7. **What happens when complete_task cannot find the requested id?**  
   **Answer:** It returns None, and the command reports the missing task as an argument error.
8. **What limitation makes a JSON file unsuitable for concurrent writers?**  
   **Answer:** Separate processes can read the same old content and overwrite each other's updates without locking or transactional coordination.

---

| [Previous: All code samples](98-all-code-samples.md) | [Notes index](../README.md) | [Next: Notes index](../README.md) |
|:--|:--:|--:|
