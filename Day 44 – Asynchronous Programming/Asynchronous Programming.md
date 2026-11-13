
# Day 44 – Asynchronous Programming with asyncio

## 1. Introduction to Asynchronous Programming

Normally, a sequential program executes one task at a time.

If a task takes time because it is waiting for a network response, file operation or another external resource, the program may remain blocked until that operation completes.

Asynchronous programming allows a program to work on other tasks while an asynchronous operation is waiting.

### Real-World Example

Imagine an application that needs to fetch information from three APIs.

Sequential execution:

1. Send request to API 1.
2. Wait for API 1.
3. Send request to API 2.
4. Wait for API 2.
5. Send request to API 3.
6. Wait for API 3.

Asynchronous execution:

1. Start API 1 request.
2. Start API 2 request.
3. Start API 3 request.
4. While requests are waiting, let other tasks make progress.
5. Collect the results as they become available.

This can reduce total waiting time when tasks are independent.

### Common Applications

- API requests.
- Network communication.
- Web servers.
- Database operations with async drivers.
- Chat applications.
- Web scraping.
- Real-time applications.
- Concurrent file or stream operations.

---

## 2. Synchronous vs Asynchronous Programming

### Synchronous Example

```python
import time


def task(name):
    print(f"{name} started")

    time.sleep(2)

    print(f"{name} completed")


start = time.perf_counter()

task("Task 1")
task("Task 2")
task("Task 3")

end = time.perf_counter()

print("Total Time:", round(end - start, 2))
```

Expected output:

```text
Task 1 started
Task 1 completed
Task 2 started
Task 2 completed
Task 3 started
Task 3 completed
Total Time: 6.0
```

Each task waits for two seconds before the next task starts.

### Asynchronous Example

Python provides the `asyncio` module for asynchronous programming.

```python
import asyncio
import time


async def task(name):
    print(f"{name} started")

    await asyncio.sleep(2)

    print(f"{name} completed")


async def main():

    await asyncio.gather(
        task("Task 1"),
        task("Task 2"),
        task("Task 3")
    )


start = time.perf_counter()

asyncio.run(main())

end = time.perf_counter()

print("Total Time:", round(end - start, 2))
```

Expected output:

```text
Task 1 started
Task 2 started
Task 3 started
Task 1 completed
Task 2 completed
Task 3 completed
Total Time: 2.0
```

The exact timing depends on the system.

All three tasks can wait concurrently rather than waiting one after another.

---

## 3. What Is a Coroutine?

A coroutine is a special function that can pause its execution and resume later.

In Python, an asynchronous function is defined using `async def`.

Example:

```python
async def greet():
    print("Hello from coroutine")
```

Calling an asynchronous function does not immediately execute its body.

Instead, it creates a coroutine object.

```python
coroutine = greet()

print(coroutine)
```

The coroutine must be awaited or scheduled to execute.

Correct example:

```python
import asyncio


async def greet():
    print("Hello from coroutine")


async def main():
    await greet()


asyncio.run(main())
```

Output:

```text
Hello from coroutine
```

### Important Difference

Normal function:

```python
def greet():
    print("Hello")
```

Asynchronous function:

```python
async def greet():
    print("Hello")
```

Calling `greet()` executes the normal function immediately.

Calling `greet()` in the asynchronous version creates a coroutine object.

---

## 4. Understanding async and await

Two important keywords are used in asynchronous Python:

- `async`
- `await`

### async

The `async` keyword defines an asynchronous function.

```python
async def download_file():
    print("Downloading file")
```

### await

The `await` keyword pauses the current coroutine until an awaitable operation completes.

```python
import asyncio


async def download_file():

    print("Download started")

    await asyncio.sleep(2)

    print("Download completed")


async def main():
    await download_file()


asyncio.run(main())
```

Output:

```text
Download started
Download completed
```

### Important Rules

1. Use `async def` to define a coroutine function.
2. Use `await` with an awaitable object.
3. `await` is normally used inside an asynchronous function.
4. `await` does not automatically create parallel execution.
5. A coroutine must be awaited or scheduled to run.

---

## 5. Understanding asyncio.sleep()

The `asyncio.sleep()` function pauses the current coroutine without blocking the event loop.

Example:

```python
import asyncio


async def task():
    print("Task started")

    await asyncio.sleep(3)

    print("Task completed")


asyncio.run(task())
```

Output:

```text
Task started
Task completed
```

### Difference Between time.sleep() and asyncio.sleep()

| time.sleep() | asyncio.sleep() |
|---|---|
| Blocks the current thread | Suspends the current coroutine |
| Does not cooperate with asyncio event loop | Allows other coroutines to run |
| Synchronous function | Asynchronous function |
| Used in synchronous programs | Used in asyncio programs |

Avoid using `time.sleep()` inside an asynchronous function when you intend to wait without blocking the event loop.

Incorrect:

```python
import asyncio
import time


async def task():
    print("Task started")

    time.sleep(3)

    print("Task completed")
```

This blocks the event loop for three seconds.

Correct:

```python
import asyncio


async def task():
    print("Task started")

    await asyncio.sleep(3)

    print("Task completed")
```

---

## 6. Understanding the Event Loop

The event loop is the central component of asyncio.

It manages asynchronous tasks and decides which coroutine should run.

When a coroutine reaches an `await` point and the awaited operation is not complete, the event loop can run another ready task.

### Simplified Working

1. Create asynchronous tasks.
2. Event loop starts managing them.
3. A task begins execution.
4. Task reaches an await point.
5. Task suspends while waiting.
6. Event loop runs another ready task.
7. Waiting task becomes ready when its operation completes.
8. Event loop resumes the task.

### Example

```python
import asyncio


async def first_task():
    print("First task started")

    await asyncio.sleep(2)

    print("First task completed")


async def second_task():
    print("Second task started")

    await asyncio.sleep(1)

    print("Second task completed")


async def main():

    await asyncio.gather(
        first_task(),
        second_task()
    )


asyncio.run(main())
```

Possible output:

```text
First task started
Second task started
Second task completed
First task completed
```

The second task finishes first because it waits for a shorter duration.

### Starting the Event Loop

The common way to start an asyncio program is:

```python
asyncio.run(main())
```

`asyncio.run()` creates and manages an event loop for the top-level coroutine, then closes the loop when execution finishes.

It should not normally be called from inside an already running event loop.

For example, in environments such as Jupyter notebooks, an event loop may already be running. In those environments, use:

```python
await main()
```

instead of calling `asyncio.run(main())` from the notebook cell.

---

## 7. Sequential Await vs Concurrent Execution

Calling coroutines one after another with `await` is still sequential.

Example:

```python
import asyncio
import time


async def task(name):
    print(f"{name} started")

    await asyncio.sleep(2)

    print(f"{name} completed")


async def main():

    await task("Task 1")
    await task("Task 2")
    await task("Task 3")


start = time.perf_counter()

asyncio.run(main())

end = time.perf_counter()

print("Total Time:", round(end - start, 2))
```

Expected output:

```text
Task 1 started
Task 1 completed
Task 2 started
Task 2 completed
Task 3 started
Task 3 completed
Total Time: 6.0
```

Each coroutine is awaited before the next one starts.

To run independent tasks concurrently, use `asyncio.gather()` or create tasks.

---

## 8. Concurrent Execution Using asyncio.gather()

`asyncio.gather()` schedules multiple awaitables and waits for their results.

Example:

```python
import asyncio


async def task(name, delay):

    print(f"{name} started")

    await asyncio.sleep(delay)

    print(f"{name} completed")

    return f"{name} result"


async def main():

    results = await asyncio.gather(
        task("Task 1", 3),
        task("Task 2", 1),
        task("Task 3", 2)
    )

    print("Results:", results)


asyncio.run(main())
```

Possible output:

```text
Task 1 started
Task 2 started
Task 3 started
Task 2 completed
Task 3 completed
Task 1 completed
Results: ['Task 1 result', 'Task 2 result', 'Task 3 result']
```

### Important gather() Behavior

- Runs multiple awaitables concurrently.
- Waits for all supplied awaitables by default.
- Returns results in the same order as the supplied awaitables.
- The order of completion can be different.
- By default, an exception from an awaitable is propagated to the caller.

### return_exceptions

You can collect exceptions as results using `return_exceptions=True`.

```python
import asyncio


async def successful_task():
    return "Success"


async def failing_task():
    raise ValueError("Something went wrong")


async def main():

    results = await asyncio.gather(
        successful_task(),
        failing_task(),
        return_exceptions=True
    )

    for result in results:
        print(result)


asyncio.run(main())
```

Possible output:

```text
Success
Something went wrong
```

The second result is an exception object, not a successful string result.

---

## 9. Creating Tasks with asyncio.create_task()

A Task schedules a coroutine to run on the event loop.

Example:

```python
import asyncio


async def download_file():
    print("Downloading...")

    await asyncio.sleep(2)

    print("Download completed")


async def main():

    task = asyncio.create_task(download_file())

    print("Task created")

    await task

    print("Main completed")


asyncio.run(main())
```

Possible output:

```text
Task created
Downloading...
Download completed
Main completed
```

### Understanding create_task()

```python
task = asyncio.create_task(download_file())
```

This schedules the coroutine to run soon on the current event loop and returns a Task object.

```python
await task
```

Waits for that task to complete.

### Multiple Tasks

```python
import asyncio


async def worker(worker_id):

    print(f"Worker {worker_id} started")

    await asyncio.sleep(2)

    print(f"Worker {worker_id} completed")


async def main():

    tasks = []

    for worker_id in range(1, 6):

        task = asyncio.create_task(
            worker(worker_id)
        )

        tasks.append(task)

    await asyncio.gather(*tasks)


asyncio.run(main())
```

All five coroutines can make progress concurrently.

---

## 10. Understanding Task and Coroutine

| Coroutine | Task |
|---|---|
| Created by calling an async function | Created by scheduling a coroutine |
| Represents asynchronous computation | Manages scheduled coroutine execution |
| Can be awaited directly | Can be awaited |
| Not automatically scheduled as an independent task | Scheduled on an event loop |

Example:

```python
coroutine = download_file()

task = asyncio.create_task(coroutine)
```

A coroutine object is wrapped in a Task to schedule it.

---

## 11. Using asyncio.wait()

`asyncio.wait()` waits for a collection of Tasks or Futures.

It returns two sets:

- `done`
- `pending`

Example:

```python
import asyncio


async def worker(worker_id, delay):

    await asyncio.sleep(delay)

    return f"Worker {worker_id} completed"


async def main():

    tasks = {
        asyncio.create_task(worker(1, 1)),
        asyncio.create_task(worker(2, 3)),
        asyncio.create_task(worker(3, 5))
    }

    done, pending = await asyncio.wait(
        tasks,
        timeout=2
    )

    print("Completed Tasks:", len(done))
    print("Pending Tasks:", len(pending))

    for task in done:
        print(task.result())

    for task in pending:
        task.cancel()

    await asyncio.gather(
        *pending,
        return_exceptions=True
    )


asyncio.run(main())
```

The two-second timeout means tasks that have not finished within that time remain pending.

### Important Difference

`asyncio.gather()` and `asyncio.wait()` are not identical.

| gather() | wait() |
|---|---|
| Returns results in input order | Returns done and pending sets |
| Convenient for collecting results | Useful for completion control |
| Accepts awaitables | Expects Tasks or Futures in modern Python |
| Propagates exceptions by default | Does not directly raise task exceptions |

---

## 12. Task Cancellation

A running asyncio Task can be asked to cancel.

Cancellation is cooperative. The coroutine receives `asyncio.CancelledError` at an appropriate suspension point.

Example:

```python
import asyncio


async def long_task():

    try:

        print("Long task started")

        await asyncio.sleep(10)

        print("Long task completed")

    except asyncio.CancelledError:

        print("Long task was cancelled")

        raise


async def main():

    task = asyncio.create_task(long_task())

    await asyncio.sleep(2)

    task.cancel()

    try:
        await task

    except asyncio.CancelledError:
        print("Cancellation handled by main")


asyncio.run(main())
```

Possible output:

```text
Long task started
Long task was cancelled
Cancellation handled by main
```

### Important Methods

- `task.cancel()` requests cancellation.
- `task.cancelled()` checks whether cancellation completed.
- `task.done()` checks whether the task finished.
- `task.result()` retrieves the result if completed successfully.

Do not silently swallow `CancelledError` unless the application has a deliberate reason to do so.

---

## 13. Handling Exceptions in Async Functions

Asynchronous functions can raise normal Python exceptions.

Example:

```python
import asyncio


async def divide(a: float, b: float) -> float:

    if b == 0:
        raise ValueError("Cannot divide by zero")

    return a / b


async def main():

    try:

        result = await divide(10, 0)

        print("Result:", result)

    except ValueError as error:

        print("Error:", error)


asyncio.run(main())
```

Output:

```text
Error: Cannot divide by zero
```

### Handling Errors from Multiple Tasks

```python
import asyncio


async def task_one():
    await asyncio.sleep(1)
    return "Task One Success"


async def task_two():
    await asyncio.sleep(1)
    raise ValueError("Task Two Failed")


async def main():

    results = await asyncio.gather(
        task_one(),
        task_two(),
        return_exceptions=True
    )

    for result in results:

        if isinstance(result, Exception):
            print("Error:", result)

        else:
            print("Result:", result)


asyncio.run(main())
```

Possible output:

```text
Result: Task One Success
Error: Task Two Failed
```

---

## 14. Timeout Handling

Sometimes an operation should not wait forever.

Python provides `asyncio.timeout()` in Python 3.11+.

Example:

```python
import asyncio


async def slow_operation():

    await asyncio.sleep(5)

    return "Operation completed"


async def main():

    try:

        async with asyncio.timeout(2):

            result = await slow_operation()

            print(result)

    except TimeoutError:

        print("Operation timed out")


asyncio.run(main())
```

Output:

```text
Operation timed out
```

### Alternative: asyncio.wait_for()

`asyncio.wait_for()` can also enforce a timeout.

```python
import asyncio


async def slow_operation():

    await asyncio.sleep(5)

    return "Completed"


async def main():

    try:

        result = await asyncio.wait_for(
            slow_operation(),
            timeout=2
        )

        print(result)

    except TimeoutError:

        print("Operation timed out")


asyncio.run(main())
```

Both approaches are useful for limiting how long an asynchronous operation can wait.

---

## 15. Limiting Concurrent Tasks with Semaphore

Sometimes we should not start too many operations simultaneously.

For example, an application may need to limit API requests.

`asyncio.Semaphore` controls how many coroutines can enter a protected section at once.

Example:

```python
import asyncio


semaphore = asyncio.Semaphore(2)


async def worker(worker_id):

    async with semaphore:

        print(f"Worker {worker_id} started")

        await asyncio.sleep(2)

        print(f"Worker {worker_id} completed")


async def main():

    tasks = [
        asyncio.create_task(worker(worker_id))
        for worker_id in range(1, 6)
    ]

    await asyncio.gather(*tasks)


asyncio.run(main())
```

At most two workers can be inside the semaphore-protected section at the same time.

Useful applications:

- Limiting API requests.
- Limiting simultaneous downloads.
- Controlling access to a remote service.
- Preventing excessive resource usage.

---

## 16. Async Context Managers

A context manager manages resources using `async with`.

An asynchronous context manager supports asynchronous setup and cleanup.

Example:

```python
import asyncio


class AsyncResource:

    async def __aenter__(self):

        print("Resource opened")

        await asyncio.sleep(1)

        return self

    async def __aexit__(
        self,
        exc_type,
        exc_value,
        traceback
    ):

        print("Resource closed")

        await asyncio.sleep(1)


async def main():

    async with AsyncResource():

        print("Using resource")


asyncio.run(main())
```

Output:

```text
Resource opened
Using resource
Resource closed
```

### Important Methods

- `__aenter__()` performs asynchronous setup.
- `__aexit__()` performs asynchronous cleanup.

This pattern is useful for asynchronous database connections, network sessions and other resources.

---

## 17. Async Iterators and Async Generators

An asynchronous iterator allows values to be produced and consumed asynchronously.

### 17.1 Async Generator

An async generator uses `async def` with `yield`.

Example:

```python
import asyncio


async def generate_numbers():

    for number in range(1, 6):

        await asyncio.sleep(1)

        yield number


async def main():

    async for number in generate_numbers():

        print(number)


asyncio.run(main())
```

Output:

```text
1
2
3
4
5
```

### 17.2 Understanding async for

Use `async for` to iterate over an asynchronous iterable.

```python
async for item in async_generator():
    print(item)
```

Unlike a normal `for` loop, `async for` can await asynchronous iteration steps.

### 17.3 Async Comprehension

Python also supports asynchronous comprehensions.

```python
import asyncio


async def generate_numbers():

    for number in range(1, 6):

        await asyncio.sleep(0.1)

        yield number


async def main():

    numbers = [
        number * 2
        async for number in generate_numbers()
    ]

    print(numbers)


asyncio.run(main())
```

Output:

```text
[2, 4, 6, 8, 10]
```

---

## 18. Understanding asyncio.Queue

`asyncio.Queue` is designed for communication between coroutines.

It is different from `queue.Queue`, which is designed for thread-based communication.

Example:

```python
import asyncio


async def producer(task_queue):

    for number in range(1, 6):

        print("Producing:", number)

        await task_queue.put(number)

    await task_queue.put(None)


async def consumer(task_queue):

    while True:

        item = await task_queue.get()

        try:

            if item is None:
                break

            print("Consuming:", item)

            await asyncio.sleep(1)

        finally:
            task_queue.task_done()


async def main():

    task_queue = asyncio.Queue()

    producer_task = asyncio.create_task(
        producer(task_queue)
    )

    consumer_task = asyncio.create_task(
        consumer(task_queue)
    )

    await producer_task

    await task_queue.join()

    await consumer_task

    print("All queue tasks completed")


asyncio.run(main())
```

Possible output:

```text
Producing: 1
Producing: 2
Producing: 3
Producing: 4
Producing: 5
Consuming: 1
Consuming: 2
Consuming: 3
Consuming: 4
Consuming: 5
All queue tasks completed
```

### Important Queue Methods

| Method | Purpose |
|---|---|
| `put()` | Add an item asynchronously |
| `get()` | Retrieve an item asynchronously |
| `task_done()` | Mark a retrieved item as completed |
| `join()` | Wait until all items are marked completed |
| `empty()` | Check whether the queue appears empty |
| `qsize()` | Return the approximate queue size |

`asyncio.Queue` is not thread-safe. Do not use it directly for communication between OS threads.

---

## 19. Asynchronous HTTP Requests

One of the most useful applications of asynchronous programming is making multiple API requests.

The popular `requests` library is synchronous.

For asynchronous HTTP operations, we can use `aiohttp` or HTTPX.

### Install aiohttp

```bash
python -m pip install aiohttp
```

### Example: Fetch Multiple API Responses

```python
import asyncio
import aiohttp


async def fetch_post(
    session: aiohttp.ClientSession,
    post_id: int
) -> dict:

    url = (
        "https://jsonplaceholder.typicode.com/posts/"
        f"{post_id}"
    )

    async with session.get(url) as response:

        response.raise_for_status()

        return await response.json()


async def main():

    async with aiohttp.ClientSession() as session:

        tasks = [
            fetch_post(session, post_id)
            for post_id in range(1, 6)
        ]

        results = await asyncio.gather(*tasks)

        for post in results:

            print(
                post["id"],
                post["title"]
            )


if __name__ == "__main__":
    asyncio.run(main())
```

Possible output:

```text
1 sunt aut facere repellat provident occaecati
2 qui est esse
3 ea molestias quasi exercitationem repellat
4 eum et est occaecati
5 nesciunt quas odio
```

The exact title text comes from the API response.

### Important Concepts

`aiohttp.ClientSession()` manages an HTTP client session.

`session.get()` creates an asynchronous HTTP request.

`async with` manages the response lifecycle.

`await response.json()` asynchronously reads and decodes the response body.

`response.raise_for_status()` raises an exception for unsuccessful HTTP status codes.

### Why Use One Session?

A session can reuse connections and manage connection pooling.

Creating a new session for every request is usually unnecessary.

---

## 20. Handling API Errors and Timeouts

Network operations can fail because of:

- Connection problems.
- Server errors.
- Invalid responses.
- Timeouts.
- DNS resolution failures.

Example:

```python
import asyncio
import aiohttp


async def fetch_data(
    session: aiohttp.ClientSession,
    url: str
) -> dict | None:

    try:

        timeout = aiohttp.ClientTimeout(total=5)

        async with session.get(
            url,
            timeout=timeout
        ) as response:

            response.raise_for_status()

            return await response.json()

    except asyncio.TimeoutError:

        print("Request timed out")

    except aiohttp.ClientError as error:

        print("Network error:", error)

    except ValueError as error:

        print("Invalid JSON:", error)

    return None


async def main():

    url = "https://jsonplaceholder.typicode.com/posts/1"

    async with aiohttp.ClientSession() as session:

        data = await fetch_data(session, url)

        if data is not None:
            print("Title:", data["title"])


if __name__ == "__main__":
    asyncio.run(main())
```

### Important Note

A real application should also validate response data before using it.

Do not assume that an API always returns the expected structure.

---

## 21. Blocking Operations Inside Async Functions

One of the most common asynchronous programming mistakes is calling blocking functions directly inside coroutines.

Example:

```python
import asyncio
import time


async def task_one():

    print("Task One Started")

    time.sleep(5)

    print("Task One Completed")


async def task_two():

    print("Task Two Started")

    await asyncio.sleep(1)

    print("Task Two Completed")


async def main():

    await asyncio.gather(
        task_one(),
        task_two()
    )


asyncio.run(main())
```

Problem:

`time.sleep(5)` blocks the event loop.

Task Two cannot make progress during that blocking period.

### Correct Version

```python
import asyncio


async def task_one():

    print("Task One Started")

    await asyncio.sleep(5)

    print("Task One Completed")


async def task_two():

    print("Task Two Started")

    await asyncio.sleep(1)

    print("Task Two Completed")


async def main():

    await asyncio.gather(
        task_one(),
        task_two()
    )


asyncio.run(main())
```

Now both tasks can make progress while waiting.

---

## 22. Running Blocking Functions in a Thread

Sometimes an application must use an existing synchronous function.

We can run blocking I/O operations in a separate thread using `asyncio.to_thread()`.

This function is available in Python 3.9+.

Example:

```python
import asyncio
import time


def blocking_operation():

    print("Blocking operation started")

    time.sleep(3)

    print("Blocking operation completed")

    return "Result received"


async def main():

    result = await asyncio.to_thread(
        blocking_operation
    )

    print(result)


asyncio.run(main())
```

Output:

```text
Blocking operation started
Blocking operation completed
Result received
```

### When to Use asyncio.to_thread()

Use it for blocking functions that would otherwise stop the event loop.

Examples:

- Legacy synchronous file operations.
- Blocking network libraries.
- Synchronous database clients.
- Other blocking I/O operations.

It does not generally make CPU-heavy Python code run in parallel because standard GIL-enabled CPython still has the GIL limitation.

---

## 23. Asyncio and Multiprocessing

Asyncio and multiprocessing solve different problems.

| Asyncio | Multiprocessing |
|---|---|
| Uses an event loop | Uses multiple processes |
| Primarily cooperative concurrency | Process-based parallel execution |
| Excellent for I/O-bound tasks | Useful for CPU-bound tasks |
| Coroutines share one thread by default | Processes have separate memory |
| Low task scheduling overhead | Higher process startup and communication overhead |

### Practical Selection

Use asyncio for:

- Multiple API requests.
- Network communication.
- Asynchronous database operations.
- Many concurrent waiting tasks.

Use multiprocessing for:

- Heavy calculations.
- CPU-intensive transformations.
- Independent parallel workloads.

They can also be combined when an application has both I/O-bound and CPU-bound work, but the architecture should be designed carefully.

---

## 24. Performance Comparison

We can compare sequential and asynchronous waiting operations.

```python
import asyncio
import time


async def async_task():
    await asyncio.sleep(2)


async def run_async():

    await asyncio.gather(
        async_task(),
        async_task(),
        async_task()
    )


def run_sequential():

    time.sleep(2)
    time.sleep(2)
    time.sleep(2)


if __name__ == "__main__":

    start = time.perf_counter()

    run_sequential()

    sequential_time = time.perf_counter() - start

    start = time.perf_counter()

    asyncio.run(run_async())

    asynchronous_time = time.perf_counter() - start

    print(
        "Sequential:",
        round(sequential_time, 2),
        "seconds"
    )

    print(
        "Asynchronous:",
        round(asynchronous_time, 2),
        "seconds"
    )
```

Expected approximate output:

```text
Sequential: 6.0 seconds
Asynchronous: 2.0 seconds
```

This example demonstrates overlapping waiting time.

It does not mean asyncio makes every Python operation three times faster.

The benefit depends on the workload.

---

## 25. Common Asyncio Mistakes

### Mistake 1: Calling Async Function Without Awaiting

Incorrect:

```python
async def greet():
    print("Hello")


greet()
```

This creates a coroutine object but does not execute it.

Correct:

```python
import asyncio


async def greet():
    print("Hello")


asyncio.run(greet())
```

### Mistake 2: Using time.sleep()

Incorrect:

```python
async def task():
    time.sleep(2)
```

Correct:

```python
async def task():
    await asyncio.sleep(2)
```

### Mistake 3: Forgetting await

Incorrect:

```python
result = fetch_data()
```

Correct:

```python
result = await fetch_data()
```

### Mistake 4: Using asyncio.run() Inside an Existing Event Loop

Incorrect in an environment where an event loop is already running:

```python
asyncio.run(main())
```

Use:

```python
await main()
```

### Mistake 5: Creating Tasks Without Managing Them

Avoid creating background tasks and then exiting without waiting for or otherwise managing their completion.

Correct approach:

```python
task = asyncio.create_task(worker())

await task
```

### Mistake 6: Using Blocking Libraries Directly

A synchronous HTTP request or blocking database call can stop the event loop.

Use an asynchronous library or move the blocking operation to a worker thread.

---

## 26. Practical Program – Async Countdown Timer

```python
import asyncio


async def countdown(name: str, seconds: int) -> None:

    for remaining in range(seconds, 0, -1):

        print(f"{name}: {remaining}")

        await asyncio.sleep(1)

    print(f"{name}: Completed")


async def main():

    await asyncio.gather(
        countdown("Timer A", 5),
        countdown("Timer B", 3),
        countdown("Timer C", 4)
    )


asyncio.run(main())
```

Possible output:

```text
Timer A: 5
Timer B: 3
Timer C: 4
Timer A: 4
Timer B: 2
Timer C: 3
...
Timer B: Completed
...
Timer C: Completed
...
Timer A: Completed
```

The output order may vary.

---

## 27. Practical Program – Async Task Manager

```python
import asyncio


async def execute_task(
    task_id: int,
    delay: int
) -> str:

    print(f"Task {task_id} started")

    await asyncio.sleep(delay)

    print(f"Task {task_id} completed")

    return f"Task {task_id} result"


async def main():

    task_details = [
        (1, 3),
        (2, 1),
        (3, 2),
        (4, 4)
    ]

    tasks = [
        asyncio.create_task(
            execute_task(task_id, delay)
        )
        for task_id, delay in task_details
    ]

    results = await asyncio.gather(*tasks)

    print("\n===== TASK REPORT =====")

    for result in results:
        print(result)


asyncio.run(main())
```

Possible output:

```text
Task 1 started
Task 2 started
Task 3 started
Task 4 started
Task 2 completed
Task 3 completed
Task 1 completed
Task 4 completed

===== TASK REPORT =====
Task 1 result
Task 2 result
Task 3 result
Task 4 result
```

---

## 28. Mini Project – Async API Data Collector

### Project Description

Build an application that retrieves multiple posts from a public API concurrently and generates a report.

The project should:

1. Fetch multiple posts.
2. Use asynchronous HTTP requests.
3. Reuse one HTTP session.
4. Limit concurrent requests.
5. Handle timeouts.
6. Handle HTTP and network errors.
7. Store successful responses.
8. Calculate total collected posts.
9. Generate a JSON report.
10. Display a summary.

### Project Structure

```text
Day-44/
│
└── AsyncAPICollector/
    │
    └── main.py
```

### Install Dependency

```bash
python -m pip install aiohttp
```

### main.py

```python
import asyncio
import aiohttp
import json
from pathlib import Path


API_URL = "https://jsonplaceholder.typicode.com/posts"

MAX_CONCURRENT_REQUESTS = 5

OUTPUT_FILE = Path("api_report.json")


async def fetch_post(
    session: aiohttp.ClientSession,
    semaphore: asyncio.Semaphore,
    post_id: int
) -> dict | None:
    """Fetch one post from the API."""

    url = f"{API_URL}/{post_id}"

    async with semaphore:

        try:

            async with session.get(url) as response:

                response.raise_for_status()

                data = await response.json()

                print(f"Post {post_id} collected")

                return data

        except asyncio.TimeoutError:

            print(f"Post {post_id}: Request timed out")

        except aiohttp.ClientError as error:

            print(f"Post {post_id}: Network error - {error}")

        except (ValueError, TypeError) as error:

            print(f"Post {post_id}: Invalid response - {error}")

    return None


async def collect_posts(
    post_ids: list[int]
) -> list[dict]:
    """Collect multiple posts concurrently."""

    timeout = aiohttp.ClientTimeout(total=10)

    semaphore = asyncio.Semaphore(
        MAX_CONCURRENT_REQUESTS
    )

    async with aiohttp.ClientSession(
        timeout=timeout
    ) as session:

        tasks = [
            fetch_post(
                session,
                semaphore,
                post_id
            )
            for post_id in post_ids
        ]

        results = await asyncio.gather(*tasks)

    return [
        result
        for result in results
        if result is not None
    ]


def generate_report(posts: list[dict]) -> dict:
    """Generate a summary of collected posts."""

    user_ids = {
        post["userId"]
        for post in posts
    }

    return {
        "total_posts": len(posts),
        "unique_users": len(user_ids),
        "posts": posts
    }


def save_report(report: dict) -> None:
    """Save collected data as a JSON file."""

    with OUTPUT_FILE.open(
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            report,
            file,
            indent=4
        )


async def main() -> None:
    """Run the asynchronous API collector."""

    post_ids = list(range(1, 21))

    print("Starting API collection...")

    collected_posts = await collect_posts(post_ids)

    report = generate_report(collected_posts)

    save_report(report)

    print("\n===== API COLLECTION REPORT =====")

    print(
        "Requested Posts:",
        len(post_ids)
    )

    print(
        "Collected Posts:",
        report["total_posts"]
    )

    print(
        "Unique Users:",
        report["unique_users"]
    )

    print(
        "Failed Requests:",
        len(post_ids) - report["total_posts"]
    )

    print(
        "Report Saved:",
        OUTPUT_FILE
    )


if __name__ == "__main__":
    asyncio.run(main())
```

### Run the Project

```bash
python main.py
```

### Expected Output Format

```text
Starting API collection...

Post 1 collected
Post 3 collected
Post 2 collected
...

===== API COLLECTION REPORT =====

Requested Posts: 20
Collected Posts: 20
Unique Users: 10
Failed Requests: 0
Report Saved: api_report.json
```

The order of collected messages can vary.

The API must be reachable for successful requests. The report may contain fewer than 20 posts if requests fail.

### Project Challenges

1. Allow users to enter the number of posts to collect.
2. Allow users to specify the maximum concurrent requests.
3. Add retry logic for temporary failures.
4. Add a request timeout option.
5. Save failed post IDs in a separate JSON file.
6. Calculate the average post title length.
7. Generate a report grouped by user ID.
8. Add logging instead of relying only on print statements.
9. Add type checking and input validation.
10. Compare sequential API requests with asynchronous requests.

---

## 29. Student Practice Exercises

### Beginner Level

1. Create your first coroutine using `async def`.
2. Use `await asyncio.sleep()`.
3. Run a coroutine using `asyncio.run()`.
4. Create two coroutines and execute them sequentially.
5. Execute three coroutines using `asyncio.gather()`.
6. Create five tasks using `asyncio.create_task()`.
7. Return values from asynchronous functions.

### Intermediate Level

8. Use `asyncio.wait()` to identify completed tasks.
9. Cancel a running task.
10. Handle exceptions in an asynchronous function.
11. Use `asyncio.wait_for()` to implement a timeout.
12. Limit concurrent operations using `asyncio.Semaphore`.
13. Build an asynchronous producer-consumer system using `asyncio.Queue`.
14. Create an async generator.
15. Implement an async context manager.
16. Run a blocking operation using `asyncio.to_thread()`.

### Advanced Level

17. Fetch multiple API responses using aiohttp.
18. Implement API request retries.
19. Build an asynchronous file processing workflow.
20. Compare synchronous and asynchronous API requests.
21. Build an async task scheduler.
22. Implement cancellation and graceful cleanup.
23. Build a concurrent API monitoring system.

---

## 30. Trainer Assessment

| Assessment Area | Expected Performance |
|---|---|
| Async Concepts | Explains asynchronous programming |
| Coroutines | Creates and executes coroutines |
| async/await | Uses both keywords correctly |
| Event Loop | Understands event loop execution |
| gather() | Runs multiple awaitables concurrently |
| Tasks | Uses create_task() and Future results |
| Cancellation | Handles task cancellation |
| Exceptions | Handles asynchronous errors |
| Timeouts | Uses timeout mechanisms |
| Semaphore | Limits concurrent operations |
| Async Generators | Uses async for and async yield |
| Async Queue | Implements producer-consumer communication |
| Async HTTP | Fetches API data with aiohttp |
| Mini Project | Completes Async API Data Collector |

---

## 31. Completion Criteria

Day 44 is complete when the student can:

- Explain asynchronous programming.
- Differentiate synchronous and asynchronous execution.
- Understand concurrency and parallelism.
- Create coroutines using `async def`.
- Use `await` correctly.
- Explain the role of an event loop.
- Use `asyncio.run()`.
- Execute multiple tasks using `asyncio.gather()`.
- Schedule tasks using `asyncio.create_task()`.
- Use `asyncio.wait()`.
- Handle task cancellation and exceptions.
- Implement timeout handling.
- Use asynchronous Semaphore and Queue.
- Create async generators and context managers.
- Fetch multiple API responses using aiohttp.
- Identify blocking operations.
- Use `asyncio.to_thread()` when appropriate.
- Complete the Async API Data Collector.

**Day 44 Completed – Asynchronous Programming with asyncio**
