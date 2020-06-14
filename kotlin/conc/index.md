./[curric](/curric)/[kotlin](/curric/kotlin)/[Concurrency](/curric/kotlin/conc)/
# Concurrency Returns
## Coroutines (The Kotlin Approach)
### What are Coroutines
Kotlin Docs for: [Basics of Coroutines](https://kotlinlang.org/docs/reference/coroutines/basics.html)

## Cancellations and Timeouts
Kotlin Docs for: [Cancellations and Timeouts](https://kotlinlang.org/docs/reference/coroutines/cancellation-and-timeouts.html)

## Suspending Functions
Kotlin Docs for: [Suspending Functions](https://kotlinlang.org/docs/reference/coroutines/composing-suspending-functions.html)

## Coroutine Context and Dispatchers
Kotlin Docs for: [Coroutine Context and Dispatchers](https://kotlinlang.org/docs/reference/coroutines/coroutine-context-and-dispatchers.html)

## Flow, Channels and Pipelines
Kotlin Docs for:
- [Asynchronous Flow](https://kotlinlang.org/docs/reference/coroutines/flow.html)
- [Channels](https://kotlinlang.org/docs/reference/coroutines/channels.html)

## Exception Handling
Kotlin Docs for: [Exception Handling](https://kotlinlang.org/docs/reference/coroutines/exception-handling.html)

## Shared Mutable State and Concurrency
Kotlin Docs for: [Shared Mutable State and Concurrency](https://kotlinlang.org/docs/reference/coroutines/shared-mutable-state-and-concurrency.html)

## Threads VS Coroutines
As Kotlin is able to target the JVM and has very stable Java interop, Threads are still able to be used. Meaning now there are two different forms of Concurrency available.

Now the question becomes which do you use? Well, it depends on the situation, each have their own pros and cons. Threads are preemptively multitasked and provide concurrency and along with parallelism. Coroutines, on the ohter hand, are cooperatively multitasked and provide concurrency but do not provide parallelism. This means that coroutines have no need for support from the underlying OS. All in all, threads have their uses and so do coroutines and its important to understand which is better for which situation.