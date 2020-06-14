./[curric](/curric)/[Concurrency](/curric/conc)/
# Concurrency
Concurrency, in the context of computer science, is the ability for a program to be decomposed into parts that can run independently of each other. This means that tasks can be executed out of order and the result would still be the same as if they are executed in order. It is the ability of an algorithm or program to run more than one task at a time. The concept is similar to parallel processing, but with the possibility of many independent jobs doing different things at once rather than executing the same job.

## Synchronous vs Asynchronous Code
- Synchronous Code
    - Synchronous Code is code that is executed sequentially, and if a section of code is considered "blocking" then the entire sequence of code will stop and wait until the "blocking" section finishes.
    > _Blocking Code is code that stops the rest of the program until the sequence of blocking code is complete. Most common examples of blocking code are loops and sleep statements_.
- Asynchronous Code
    - Asynchronous Code is code that is executed concurrently with the rest of the code. Asynchronous code eliminates the need to wait for previous blocking calls to complete. This allows for greater time optimizations and allows for multiple tasks to run in parallel. A rule of thumb with asynchronous code is that every separate _thread_ doesn't affect another.

### [Threads](./thread)