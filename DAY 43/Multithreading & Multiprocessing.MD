
# Day 43 – Multithreading & Multiprocessing

## 1. Introduction to Concurrency

Normally, Python programs execute instructions sequentially.

This means one operation completes before the next operation starts.

Example:

```python
def task_one():
    print("Task One Started")
    print("Task One Completed")


def task_two():
    print("Task Two Started")
    print("Task Two Completed")


task_one()
task_two()
```

Output:

```text
Task One Started
Task One Completed
Task Two Started
Task Two Completed
```

For programs with multiple independent tasks, sequential execution may not always be efficient.

Python provides different ways to manage multiple tasks.

Two important approaches are:

1. Multithreading
2. Multiprocessing

---

## 2. What Is Concurrency?

Concurrency means managing multiple tasks during overlapping periods of time.

Tasks make progress without necessarily running at the exact same instant.

Example:

- Downloading a file.
- Reading another file.
- Waiting for an API response.
- Updating application information.

A concurrent program can switch between tasks while other tasks are waiting.

## 3. What Is Parallelism?

Parallelism means executing multiple tasks at the same instant using multiple processing resources, such as different CPU cores.

Example:

- Processing image 1 on one CPU core.
- Processing image 2 on another CPU core.
- Processing image 3 on another CPU core.

### Concurrency vs Parallelism

| Concurrency | Parallelism |
|---|---|
| Multiple tasks make progress | Multiple tasks execute simultaneously |
| Tasks may take turns | Tasks can execute at the same instant |
| Useful for overlapping operations | Useful for CPU-intensive work |
| Does not require multiple CPU cores | Typically uses multiple processing resources |

Concurrency is about task coordination. Parallelism is about simultaneous execution.

---

## 4. What Is a Thread?

A thread is a smaller unit of execution inside a process.

A process can contain one or multiple threads.

Threads inside the same process share memory and resources.

Example:

A music application may use different threads for:

- Playing audio.
- Downloading music.
- Updating the user interface.
- Loading album information.

Python provides the `threading` module for multithreading.

### Important Thread Characteristics

- Threads belong to a process.
- Threads share the process's memory.
- Threads are relatively lightweight compared with processes.
- Threads are useful for I/O-bound tasks.
- Shared memory can create race conditions.

---

## 5. Creating Your First Thread

Import the `threading` module.

```python
import threading


def display_message():
    print("Hello from a separate thread")


thread = threading.Thread(target=display_message)

thread.start()

thread.join()

print("Main program completed")
```

Possible output:

```text
Hello from a separate thread
Main program completed
```

### Explanation

`threading.Thread()` creates a thread object.

`target` specifies the function that the thread should execute.

`start()` starts the thread.

`join()` makes the calling thread wait until the target thread finishes.

### Important Difference

Do not call the target function directly when creating the thread.

Incorrect:

```python
thread = threading.Thread(
    target=display_message()
)
```

Correct:

```python
thread = threading.Thread(
    target=display_message
)
```

The function is passed as an object, not executed immediately.

---

## 6. Running Multiple Threads

We can create multiple threads to execute different tasks.

```python
import threading
import time


def task(name):
    print(f"{name} started")

    time.sleep(2)

    print(f"{name} completed")


thread_one = threading.Thread(
    target=task,
    args=("Task One",)
)

thread_two = threading.Thread(
    target=task,
    args=("Task Two",)
)

thread_one.start()
thread_two.start()

thread_one.join()
thread_two.join()

print("All tasks completed")
```

Possible output:

```text
Task One started
Task Two started
Task One completed
Task Two completed
All tasks completed
```

The order of messages may vary because thread scheduling is controlled by the operating system and Python runtime.

### Understanding args

`args` passes positional arguments to the target function.

```python
args=("Task One",)
```

The comma is important because a single-element tuple requires a trailing comma.

---

## 7. Main Thread and Current Thread

Every Python program starts with a main thread.

We can inspect thread information using `threading.current_thread()`.

```python
import threading


def display_thread():
    current = threading.current_thread()

    print("Thread Name:", current.name)
    print("Thread ID:", current.ident)


print("Main Thread:", threading.current_thread().name)

thread = threading.Thread(
    target=display_thread,
    name="Worker-1"
)

thread.start()
thread.join()
```

Possible output:

```text
Main Thread: MainThread
Thread Name: Worker-1
Thread ID: 123456
```

The numeric thread ID is system-dependent.

### Useful Thread Properties

```python
thread.name
thread.ident
thread.is_alive()
thread.daemon
```

`is_alive()` checks whether the thread is currently running.

---

## 8. Threading with a Loop

We can create multiple threads dynamically using a loop.

```python
import threading
import time


def worker(worker_id):
    print(f"Worker {worker_id} started")

    time.sleep(1)

    print(f"Worker {worker_id} finished")


threads = []

for worker_id in range(1, 6):

    thread = threading.Thread(
        target=worker,
        args=(worker_id,)
    )

    threads.append(thread)
    thread.start()


for thread in threads:
    thread.join()


print("All workers finished")
```

Possible output:

```text
Worker 1 started
Worker 2 started
Worker 3 started
Worker 4 started
Worker 5 started
Worker 1 finished
Worker 2 finished
Worker 3 finished
Worker 4 finished
Worker 5 finished
All workers finished
```

The exact order can differ.

---

## 9. Daemon and Non-Daemon Threads

Python threads can be daemon or non-daemon threads.

### Non-Daemon Thread

A non-daemon thread keeps the Python process alive until it finishes.

It is the default behavior.

```python
import threading
import time


def worker():
    time.sleep(2)
    print("Worker completed")


thread = threading.Thread(target=worker)

thread.start()

print("Main program finished")
```

The program waits for the worker thread to finish before exiting.

### Daemon Thread

A daemon thread does not prevent the Python process from exiting.

When no non-daemon work remains, daemon threads may be stopped abruptly.

```python
import threading
import time


def background_task():
    while True:
        print("Background task running")
        time.sleep(1)


thread = threading.Thread(
    target=background_task,
    daemon=True
)

thread.start()

print("Main program completed")
```

The program can exit without waiting for the daemon thread.

### Important Note

Use daemon threads only for background tasks that can safely stop when the program exits.

Do not depend on daemon threads to complete important database writes, file operations or financial transactions.

---

## 10. The Global Interpreter Lock (GIL)

The Global Interpreter Lock, commonly called GIL, is an important concept in traditional CPython builds.

In a standard GIL-enabled CPython interpreter, the GIL allows only one thread at a time to execute Python bytecode within a given interpreter.

This affects CPU-bound multithreaded programs.

### CPU-Bound Tasks

CPU-bound tasks spend most of their time performing calculations.

Examples:

- Large mathematical calculations.
- Image processing.
- Video encoding.
- Data transformations.
- Complex simulations.

In a standard GIL-enabled CPython build, multiple threads generally do not provide true parallel execution of Python bytecode.

### I/O-Bound Tasks

I/O-bound tasks spend much of their time waiting for external operations.

Examples:

- Network requests.
- File operations.
- Database communication.
- API calls.
- Waiting for user input.

Threads can be useful for I/O-bound tasks because the interpreter can switch to other threads while one is waiting.

### Important Modern Python Note

Python also has optional free-threaded CPython builds that can run without the traditional GIL. Their availability and compatibility depend on the Python version and installed packages.

For this lesson, assume a standard GIL-enabled CPython build unless stated otherwise.

---

## 11. What Is a Race Condition?

A race condition occurs when multiple threads access shared data and the final result depends on the timing or order of their operations.

Example:

```python
import threading


counter = 0


def increment():
    global counter

    for _ in range(100000):
        counter += 1


thread_one = threading.Thread(target=increment)
thread_two = threading.Thread(target=increment)

thread_one.start()
thread_two.start()

thread_one.join()
thread_two.join()

print("Final Counter:", counter)
```

The expected mathematical result is:

```text
Final Counter: 200000
```

However, shared read-modify-write operations should not be assumed to be safe just because the GIL exists.

The result can depend on implementation details and execution timing.

We should protect shared mutable state when multiple threads access it.

---

## 12. Thread Synchronization Using Lock

A lock is used to protect shared resources.

Only one thread can hold a standard `threading.Lock` at a time.

Example:

```python
import threading


counter = 0

lock = threading.Lock()


def increment():
    global counter

    for _ in range(100000):

        with lock:
            counter += 1


thread_one = threading.Thread(target=increment)
thread_two = threading.Thread(target=increment)

thread_one.start()
thread_two.start()

thread_one.join()
thread_two.join()

print("Final Counter:", counter)
```

Output:

```text
Final Counter: 200000
```

### Understanding Lock

```python
lock = threading.Lock()
```

Creates a lock.

```python
with lock:
```

Acquires the lock before entering the block and releases it automatically when leaving the block.

This is safer than manually acquiring and releasing a lock in every situation.

### Important Rule

Keep locked sections as small as practical.

Holding a lock for too long can reduce concurrency and create performance problems.

---

## 13. RLock – Reentrant Lock

A regular Lock cannot be acquired repeatedly by the same thread without first releasing it.

An `RLock` allows the same thread to acquire the lock multiple times.

```python
import threading


lock = threading.RLock()


def task():
    with lock:
        print("First lock acquired")

        with lock:
            print("Second lock acquired")


thread = threading.Thread(target=task)

thread.start()
thread.join()
```

Output:

```text
First lock acquired
Second lock acquired
```

An RLock tracks how many times the owning thread has acquired it. The thread must release it the same number of times.

Use RLock only when reentrant locking is needed.

---

## 14. Semaphore

A semaphore controls access to a resource using a counter.

It allows a limited number of threads to enter a protected section at the same time.

Example:

```python
import threading
import time


semaphore = threading.Semaphore(2)


def access_resource(worker_id):

    with semaphore:

        print(f"Worker {worker_id} entered")

        time.sleep(2)

        print(f"Worker {worker_id} left")


threads = []

for worker_id in range(1, 6):

    thread = threading.Thread(
        target=access_resource,
        args=(worker_id,)
    )

    threads.append(thread)
    thread.start()


for thread in threads:
    thread.join()


print("All workers completed")
```

At most two workers can be inside the protected section at the same time.

Useful applications:

- Limiting simultaneous API requests.
- Restricting database connections.
- Controlling access to limited resources.

---

## 15. Event – Thread Communication

An Event allows threads to communicate through a shared signal.

One thread can wait until another thread sets the event.

```python
import threading
import time


event = threading.Event()


def worker():

    print("Worker waiting for signal")

    event.wait()

    print("Signal received. Worker continuing")


thread = threading.Thread(target=worker)

thread.start()

time.sleep(2)

print("Sending signal")

event.set()

thread.join()
```

Output:

```text
Worker waiting for signal
Sending signal
Signal received. Worker continuing
```

Useful Event methods:

- `set()` – Set the event signal.
- `clear()` – Reset the event.
- `wait()` – Wait until the event is set.
- `is_set()` – Check the event state.

---

## 16. Queue for Thread Communication

The `queue` module provides thread-safe queues.

A queue is useful when one thread produces data and another thread consumes it.

This is called the Producer-Consumer pattern.

```python
import threading
import queue
import time


task_queue = queue.Queue()


def producer():

    for number in range(1, 6):

        print("Producing:", number)

        task_queue.put(number)

    task_queue.put(None)


def consumer():

    while True:

        item = task_queue.get()

        try:

            if item is None:
                break

            print("Consuming:", item)

            time.sleep(1)

        finally:
            task_queue.task_done()


producer_thread = threading.Thread(target=producer)
consumer_thread = threading.Thread(target=consumer)

producer_thread.start()
consumer_thread.start()

producer_thread.join()
task_queue.join()
consumer_thread.join()

print("Producer and consumer completed")
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
Producer and consumer completed
```

The exact interleaving may vary.

### Important Queue Methods

| Method | Purpose |
|---|---|
| `put(item)` | Add an item |
| `get()` | Retrieve an item |
| `task_done()` | Mark a retrieved task as completed |
| `join()` | Wait until all queued tasks are marked completed |
| `empty()` | Check whether the queue appears empty |
| `qsize()` | Return the approximate queue size |

For coordination between threads, use Queue instead of manually sharing a list whenever possible.

---

## 17. ThreadPoolExecutor

Creating and managing many threads manually can become difficult.

Python provides `ThreadPoolExecutor` through the `concurrent.futures` module.

It manages a pool of worker threads.

```python
from concurrent.futures import ThreadPoolExecutor
import time


def download_file(file_name: str) -> str:

    print(f"Downloading {file_name}")

    time.sleep(2)

    return f"{file_name} downloaded"


with ThreadPoolExecutor(max_workers=3) as executor:

    results = executor.map(
        download_file,
        ["file1.zip", "file2.zip", "file3.zip", "file4.zip"]
    )

    for result in results:
        print(result)
```

Possible output:

```text
Downloading file1.zip
Downloading file2.zip
Downloading file3.zip
Downloading file4.zip
file1.zip downloaded
file2.zip downloaded
file3.zip downloaded
file4.zip downloaded
```

The executor starts up to three worker threads for this example.

### Important Concepts

`max_workers` specifies the maximum number of workers.

`executor.map()` applies a function to multiple input values.

The result iterator yields results in the order of the input items.

### Submit and Future

`submit()` schedules an individual task and returns a Future object.

```python
from concurrent.futures import ThreadPoolExecutor
import time


def calculate_square(number: int) -> int:

    time.sleep(1)

    return number * number


with ThreadPoolExecutor(max_workers=3) as executor:

    future = executor.submit(calculate_square, 5)

    print("Task submitted")

    result = future.result()

    print("Result:", result)
```

Output:

```text
Task submitted
Result: 25
```

`future.result()` waits for the task to finish and returns its result.

If the task raises an exception, calling `result()` raises that exception.

---

## 18. What Is a Process?

A process is an independent running instance of a program.

Each process has its own memory space and Python interpreter.

A process can contain one or multiple threads.

Examples:

- Running a web browser.
- Running a text editor.
- Running a Python script.
- Running a database server.

Python provides the `multiprocessing` module to create multiple processes.

### Thread vs Process

| Thread | Process |
|---|---|
| Part of a process | Independent program execution |
| Shares process memory | Has separate memory space |
| Lower creation overhead | Higher creation overhead |
| Communication can use shared objects | Communication often uses IPC |
| Useful for I/O-bound tasks | Useful for CPU-bound tasks |
| Threads can be affected by the GIL | Separate processes can execute Python code in parallel |

---

## 19. Creating Your First Process

```python
import multiprocessing


def display_message():
    print("Hello from another process")


if __name__ == "__main__":

    process = multiprocessing.Process(
        target=display_message
    )

    process.start()

    process.join()

    print("Main process completed")
```

Output:

```text
Hello from another process
Main process completed
```

### Understanding Process Methods

`multiprocessing.Process()` creates a process object.

`start()` starts the child process.

`join()` waits for the child process to finish.

`is_alive()` checks whether the process is still running.

`terminate()` requests process termination.

### Why Use the Main Guard?

Always protect process creation with:

```python
if __name__ == "__main__":
```

This is especially important on Windows, where child processes use the spawn start method by default.

Without the main guard, child processes may try to execute the process-creation code again.

---

## 20. Running Multiple Processes

```python
import multiprocessing
import time


def worker(worker_id):

    print(f"Process {worker_id} started")

    time.sleep(2)

    print(f"Process {worker_id} completed")


if __name__ == "__main__":

    processes = []

    for worker_id in range(1, 4):

        process = multiprocessing.Process(
            target=worker,
            args=(worker_id,)
        )

        processes.append(process)

        process.start()

    for process in processes:
        process.join()

    print("All processes completed")
```

Possible output:

```text
Process 1 started
Process 2 started
Process 3 started
Process 1 completed
Process 2 completed
Process 3 completed
All processes completed
```

Output order can vary.

---

## 21. Multiprocessing with Pool

When processing many independent tasks, creating one process per task may be inefficient.

A process pool reuses a limited number of worker processes.

```python
import multiprocessing


def calculate_square(number: int) -> int:
    return number * number


if __name__ == "__main__":

    numbers = [1, 2, 3, 4, 5, 6]

    with multiprocessing.Pool(processes=3) as pool:

        results = pool.map(
            calculate_square,
            numbers
        )

    print(results)
```

Output:

```text
[1, 4, 9, 16, 25, 36]
```

### Important Pool Methods

| Method | Purpose |
|---|---|
| `map()` | Apply a function to multiple inputs |
| `starmap()` | Apply a function using multiple arguments per input |
| `apply()` | Execute a function with one input set |
| `apply_async()` | Schedule a task asynchronously |
| `close()` | Prevent additional tasks from being submitted |
| `join()` | Wait for worker processes to finish |

Using a Pool as a context manager automatically manages its lifecycle.

---

## 22. ProcessPoolExecutor

`ProcessPoolExecutor` provides a high-level interface for process-based parallelism.

```python
from concurrent.futures import ProcessPoolExecutor


def calculate_square(number: int) -> int:
    return number * number


if __name__ == "__main__":

    numbers = [10, 20, 30, 40, 50]

    with ProcessPoolExecutor(max_workers=3) as executor:

        results = executor.map(
            calculate_square,
            numbers
        )

        print(list(results))
```

Output:

```text
[100, 400, 900, 1600, 2500]
```

### Why Use ProcessPoolExecutor?

- Manages worker processes.
- Provides Future objects.
- Supports `submit()` and `map()`.
- Handles worker lifecycle.
- Offers an interface similar to ThreadPoolExecutor.

Functions and arguments used with process pools generally need to be picklable.

Define worker functions at module level for reliable multiprocessing, especially on Windows.

---

## 23. Communication Between Processes

Processes do not normally share their Python variables.

Example:

```python
import multiprocessing


def worker():
    value = 100
    print("Child Value:", value)


if __name__ == "__main__":

    value = 50

    process = multiprocessing.Process(
        target=worker
    )

    process.start()
    process.join()

    print("Parent Value:", value)
```

Output:

```text
Child Value: 100
Parent Value: 50
```

The child process has its own memory.

Changing a normal variable in one process does not automatically change the corresponding variable in another process.

Python provides several communication mechanisms.

- Queue
- Pipe
- Shared Memory
- Manager objects

---

## 24. Multiprocessing Queue

A multiprocessing Queue allows processes to exchange data.

```python
import multiprocessing


def producer(result_queue):

    for number in range(1, 6):
        result_queue.put(number)

    result_queue.put(None)


def consumer(result_queue):

    while True:

        item = result_queue.get()

        if item is None:
            break

        print("Received:", item)


if __name__ == "__main__":

    result_queue = multiprocessing.Queue()

    producer_process = multiprocessing.Process(
        target=producer,
        args=(result_queue,)
    )

    consumer_process = multiprocessing.Process(
        target=consumer,
        args=(result_queue,)
    )

    producer_process.start()
    consumer_process.start()

    producer_process.join()
    consumer_process.join()

    result_queue.close()

    print("Communication completed")
```

Output:

```text
Received: 1
Received: 2
Received: 3
Received: 4
Received: 5
Communication completed
```

The Queue uses inter-process communication rather than directly sharing ordinary Python variables.

---

## 25. Multiprocessing Pipe

A Pipe provides a communication channel between two processes.

```python
import multiprocessing


def worker(connection):

    connection.send("Hello from child process")

    connection.close()


if __name__ == "__main__":

    parent_connection, child_connection = multiprocessing.Pipe()

    process = multiprocessing.Process(
        target=worker,
        args=(child_connection,)
    )

    process.start()

    message = parent_connection.recv()

    print(message)

    process.join()

    parent_connection.close()
```

Output:

```text
Hello from child process
```

### Pipe Methods

- `send()` – Send an object.
- `recv()` – Receive an object.
- `close()` – Close the connection.

A Pipe is useful when two processes need a direct communication channel.

---

## 26. Shared Memory

Multiprocessing provides shared memory for situations where processes need to access common data without repeatedly sending copies through queues.

Python provides `multiprocessing.shared_memory`.

Example:

```python
import multiprocessing
from multiprocessing import shared_memory


def worker(shm_name):

    existing_memory = shared_memory.SharedMemory(
        name=shm_name
    )

    existing_memory.buf[0] = 100

    existing_memory.close()


if __name__ == "__main__":

    memory = shared_memory.SharedMemory(
        create=True,
        size=10
    )

    memory.buf[0] = 50

    process = multiprocessing.Process(
        target=worker,
        args=(memory.name,)
    )

    process.start()
    process.join()

    print("Shared Value:", memory.buf[0])

    memory.close()
    memory.unlink()
```

Output:

```text
Shared Value: 100
```

### Important Shared Memory Rules

- Both processes must know the shared memory name.
- Shared memory should be closed when no longer needed.
- The process responsible for creating it should unlink it when finished.
- Shared mutable data may require synchronization.
- Always handle cleanup, including when errors occur.

Shared memory is useful for large data structures and high-performance inter-process communication.

---

## 27. Process Synchronization with Lock

Multiple processes may also access shared resources.

A multiprocessing Lock can protect shared state.

```python
import multiprocessing


def increment(counter, lock):

    for _ in range(1000):

        with lock:
            counter.value += 1


if __name__ == "__main__":

    counter = multiprocessing.Value("i", 0)

    lock = multiprocessing.Lock()

    processes = []

    for _ in range(4):

        process = multiprocessing.Process(
            target=increment,
            args=(counter, lock)
        )

        processes.append(process)
        process.start()

    for process in processes:
        process.join()

    print("Final Counter:", counter.value)
```

Output:

```text
Final Counter: 4000
```

### Understanding multiprocessing.Value

`multiprocessing.Value()` creates a shared value.

`"i"` indicates a signed integer type.

The Lock protects the read-modify-write operation.

---

## 28. Deadlock

A deadlock occurs when two or more tasks wait indefinitely for resources held by one another.

Example situation:

- Thread A holds Lock 1 and waits for Lock 2.
- Thread B holds Lock 2 and waits for Lock 1.

Neither thread can continue.

### Example of Deadlock Structure

```python
import threading


lock_one = threading.Lock()
lock_two = threading.Lock()


def task_one():

    with lock_one:

        print("Task One acquired Lock One")

        with lock_two:
            print("Task One acquired Lock Two")


def task_two():

    with lock_two:

        print("Task Two acquired Lock Two")

        with lock_one:
            print("Task Two acquired Lock One")


thread_one = threading.Thread(target=task_one)
thread_two = threading.Thread(target=task_two)

thread_one.start()
thread_two.start()
```

This code can deadlock. Do not run it as a normal exercise because it may hang.

### How to Prevent Deadlocks

1. Acquire locks in a consistent global order.
2. Avoid unnecessary nested locks.
3. Keep locked sections short.
4. Use timeouts when appropriate.
5. Release locks reliably using context managers.

---

## 29. When Should You Use Threads or Processes?

### Use Multithreading When

- The program performs network requests.
- Multiple files must be downloaded.
- Several API requests can run concurrently.
- Tasks spend time waiting for I/O.
- You need lightweight concurrency.

### Use Multiprocessing When

- The program performs heavy calculations.
- Multiple CPU cores can be used.
- Tasks are independent.
- True parallel execution is required in standard GIL-enabled CPython.

### Comparison

| Requirement | Recommended Approach |
|---|---|
| Download many files | Threading |
| Multiple API requests | Threading |
| CPU-heavy calculations | Multiprocessing |
| Large independent data processing | Multiprocessing |
| Shared in-process application state | Threading |
| Isolated worker execution | Multiprocessing |
| Limited concurrent access | Semaphore |
| Shared thread communication | `queue.Queue` |
| Process communication | `multiprocessing.Queue` |

The best approach depends on workload, data size, communication cost and operating environment.

---

## 30. Performance Benchmarking

Never assume that multithreading or multiprocessing is always faster.

Process creation, thread scheduling and communication introduce overhead.

We can compare different execution methods.

```python
import time
import threading
import multiprocessing
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor


def calculate_sum(number: int) -> int:

    total = 0

    for value in range(number):
        total += value

    return total


def run_sequential(numbers: list[int]) -> None:

    for number in numbers:
        calculate_sum(number)


def run_threading(numbers: list[int]) -> None:

    with ThreadPoolExecutor(max_workers=4) as executor:
        list(executor.map(calculate_sum, numbers))


def run_multiprocessing(numbers: list[int]) -> None:

    with ProcessPoolExecutor(max_workers=4) as executor:
        list(executor.map(calculate_sum, numbers))


if __name__ == "__main__":

    numbers = [5_000_000] * 4

    methods = [
        ("Sequential", run_sequential),
        ("Threading", run_threading),
        ("Multiprocessing", run_multiprocessing)
    ]

    for name, function in methods:

        start = time.perf_counter()

        function(numbers)

        end = time.perf_counter()

        print(
            f"{name}: {(end - start):.3f} seconds"
        )
```

Example output format:

```text
Sequential: X.XXX seconds
Threading: X.XXX seconds
Multiprocessing: X.XXX seconds
```

Actual timings depend on:

- CPU model and core count.
- Python version and build.
- Operating system.
- Process startup overhead.
- System load.
- Number and size of tasks.

For this CPU-bound workload, multiprocessing may outperform threading, but the result must be measured rather than assumed.

---

## 31. Practical Program – Concurrent File Processing

Create a program that processes multiple text files using threads.

### Project Structure

```text
FileProcessor/
│
├── main.py
└── files/
    ├── file1.txt
    ├── file2.txt
    └── file3.txt
```

### main.py

```python
from concurrent.futures import ThreadPoolExecutor
from pathlib import Path


def count_words(file_path: Path) -> tuple[str, int]:
    """Count words in a text file."""

    content = file_path.read_text(encoding="utf-8")

    word_count = len(content.split())

    return file_path.name, word_count


def main() -> None:

    folder = Path("files")

    file_paths = list(folder.glob("*.txt"))

    if not file_paths:
        print("No text files found.")
        return

    with ThreadPoolExecutor(max_workers=3) as executor:

        results = executor.map(
            count_words,
            file_paths
        )

        for file_name, count in results:

            print(
                f"{file_name}: {count} words"
            )


if __name__ == "__main__":
    main()
```

Example output:

```text
file1.txt: 20 words
file2.txt: 35 words
file3.txt: 18 words
```

This project demonstrates I/O-oriented concurrency.

---

## 32. Mini Project – Parallel Data Processing System

### Project Description

Build a Python application that divides a large list of numbers into smaller chunks and processes them using multiple processes.

The application should calculate:

1. Sum of all numbers.
2. Square of each number.
3. Even numbers.
4. Odd numbers.
5. Maximum value.
6. Minimum value.
7. Processing time.

### Project Structure

```text
Day-43/
│
└── ParallelDataProcessor/
    │
    └── main.py
```

### Implementation

Create `main.py`.

```python
import multiprocessing
import time


def process_chunk(numbers: list[int]) -> dict[str, int | list[int]]:
    """Process one chunk of numbers."""

    return {
        "total": sum(numbers),
        "squares": [number ** 2 for number in numbers],
        "even": [
            number for number in numbers
            if number % 2 == 0
        ],
        "odd": [
            number for number in numbers
            if number % 2 != 0
        ],
        "maximum": max(numbers) if numbers else 0,
        "minimum": min(numbers) if numbers else 0
    }


def split_into_chunks(
    numbers: list[int],
    chunk_size: int
) -> list[list[int]]:
    """Split numbers into smaller chunks."""

    return [
        numbers[index:index + chunk_size]
        for index in range(0, len(numbers), chunk_size)
    ]


def main() -> None:
    """Run the parallel data processing system."""

    numbers = list(range(1, 100001))

    chunks = split_into_chunks(
        numbers,
        10000
    )

    start_time = time.perf_counter()

    with multiprocessing.Pool(processes=4) as pool:

        results = pool.map(
            process_chunk,
            chunks
        )

    total_sum = sum(
        result["total"]
        for result in results
    )

    all_even = [
        number
        for result in results
        for number in result["even"]
    ]

    all_odd = [
        number
        for result in results
        for number in result["odd"]
    ]

    all_squares = [
        number
        for result in results
        for number in result["squares"]
    ]

    maximum = max(
        result["maximum"]
        for result in results
    )

    minimum = min(
        result["minimum"]
        for result in results
    )

    end_time = time.perf_counter()

    print("\n===== PARALLEL DATA PROCESSOR =====")

    print("Total Numbers:", len(numbers))
    print("Total Sum:", total_sum)
    print("Even Count:", len(all_even))
    print("Odd Count:", len(all_odd))
    print("Maximum:", maximum)
    print("Minimum:", minimum)

    print("First 10 Squares:", all_squares[:10])

    print(
        "Processing Time:",
        round(end_time - start_time, 4),
        "seconds"
    )


if __name__ == "__main__":
    main()
```

### Expected Output

```text
===== PARALLEL DATA PROCESSOR =====

Total Numbers: 100000
Total Sum: 5000050000
Even Count: 50000
Odd Count: 50000
Maximum: 100000
Minimum: 1
First 10 Squares: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
Processing Time: X.XXXX seconds
```

The processing time varies by system.

### Run the Project

```bash
python main.py
```

### Project Challenges

1. Allow the user to enter the number of processes.
2. Allow the user to enter the chunk size.
3. Compare sequential and multiprocessing execution.
4. Add exception handling.
5. Save the final report to a JSON file.
6. Add logging to record processing details.
7. Handle an empty input list.
8. Handle invalid chunk sizes.

---

## 33. Important Best Practices

1. Use threads primarily for I/O-bound workloads.
2. Use processes for CPU-bound workloads when parallel execution is beneficial.
3. Use `join()` when the main program must wait for workers.
4. Protect shared mutable state with synchronization.
5. Prefer queues for producer-consumer communication.
6. Avoid unnecessary global variables.
7. Avoid creating too many threads or processes.
8. Use ThreadPoolExecutor and ProcessPoolExecutor for manageable task pools.
9. Use the main guard for multiprocessing programs.
10. Avoid daemon threads for critical work.
11. Handle worker exceptions.
12. Measure performance before choosing an execution strategy.
13. Avoid deadlocks by designing synchronization carefully.
14. Clean up shared memory and other resources.
15. Keep multiprocessing worker functions at module level when possible.

---

## 34. Student Practice Exercises

### Beginner Level

1. Create a thread that prints your name.
2. Create two threads that execute different functions.
3. Create five threads using a loop.
4. Display the name of the current thread.
5. Create a process that prints a message.
6. Create three processes that execute the same function.
7. Use `join()` to wait for all workers.

### Intermediate Level

8. Create a shared counter protected by a Lock.
9. Use an RLock with nested functions.
10. Create a Semaphore that allows only two workers at a time.
11. Use Event to coordinate two threads.
12. Implement a producer-consumer system using Queue.
13. Use ThreadPoolExecutor to process ten tasks.
14. Use ProcessPoolExecutor to calculate squares.
15. Communicate between processes using Queue.
16. Exchange messages using Pipe.

### Advanced Level

17. Build a multithreaded website response simulator.
18. Create a parallel image-processing workflow.
19. Compare sequential, threaded and multiprocessing execution.
20. Build a process-safe shared counter.
21. Demonstrate a deadlock and then fix it.
22. Build a concurrent file analyzer.
23. Build a parallel data processing application.

---

## 35. Trainer Assessment

| Assessment Area | Expected Performance |
|---|---|
| Concurrency | Explains concurrency correctly |
| Parallelism | Explains parallel execution |
| Threading | Creates and manages threads |
| Thread Synchronization | Uses Lock, RLock and Semaphore |
| Communication | Uses Event and Queue |
| ThreadPoolExecutor | Executes tasks using worker pools |
| Multiprocessing | Creates and manages processes |
| Process Communication | Uses Queue and Pipe |
| Shared Memory | Understands shared-memory basics |
| Process Synchronization | Uses multiprocessing Lock |
| Performance | Compares execution strategies |
| Mini Project | Completes Parallel Data Processing System |

---

## 36. Completion Criteria

Day 43 is complete when the student can:

- Explain processes and threads.
- Differentiate concurrency and parallelism.
- Create and execute multiple threads.
- Create and execute multiple processes.
- Explain the Global Interpreter Lock.
- Identify I/O-bound and CPU-bound workloads.
- Understand race conditions.
- Use Lock, RLock and Semaphore.
- Communicate between threads using Queue and Event.
- Use ThreadPoolExecutor.
- Communicate between processes using Queue and Pipe.
- Understand shared memory.
- Use ProcessPoolExecutor and multiprocessing Pool.
- Identify and prevent deadlocks.
- Benchmark sequential, threaded and parallel execution.
- Complete the Parallel Data Processing System.

**Day 43 Completed – Multithreading & Multiprocessing**
