# asyncio
#asynchronous #python

[Link to the official docs](https://docs.python.org/3/library/asyncio-task.html)

Code example:
```python
import asyncio

async def main():
	print('hello')
	await asyncio.sleep(1)
	print('world')

asyncio.run(main())
# hello
# world
```

Functions are called *coroutines*. The preferred way to write async programs is with `async` and `await` syntax.

Assigning coroutine to a task makes it possible to run them concurrently. Following example shows the difference between regular function call and concurrent.
Regular takes 3 seconds to execute:
```python
import asyncio
import time

async def say_after(delay, what):
    await asyncio.sleep(delay)
    print(what)

async def main():
    print(f"started at {time.strftime('%X')}")
	
    await say_after(1, 'hello')
    await say_after(2, 'world')
	
    print(f"finished at {time.strftime('%X')}")

asyncio.run(main())

# started at 17:13:52
# hello
# world
# finished at 17:13:55
```

Asyncio finishes in 2 seconds:
```python
async def main():
    task1 = asyncio.create_task(
        say_after(1, 'hello'))
		
    task2 = asyncio.create_task(
        say_after(2, 'world'))
	
    print(f"started at {time.strftime('%X')}")

    # Wait until both tasks are completed (should take
    # around 2 seconds.)
    await task1
    await task2
	
    print(f"finished at {time.strftime('%X')}")

# started at 17:14:32
# hello
# world
# finished at 17:14:34
```

Python version 3.11 adds class `asyncio.TaskGroup`:
```python
async def main():
    async with asyncio.TaskGroup() as tg:
        task1 = tg.create_task(
            say_after(1, 'hello'))
			
        task2 = tg.create_task(
            say_after(2, 'world'))
			
        print(f"started at {time.strftime('%X')}")

    # The wait is implicit when the context manager exits.
	
    print(f"finished at {time.strftime('%X')}")
```