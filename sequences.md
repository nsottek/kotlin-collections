[kotlin-blog]: https://blog.kotlin-academy.com/effective-kotlin-use-sequence-for-bigger-collections-with-more-than-one-processing-step-649a15bb4bf
[sequences-speed-article]: https://medium.com/@elye.project/kotlin-slow-list-and-lazy-sequence-61691fc974c5
## `Sequences`
So for most of the previous examples of operators in [`Lap 3`](/operators.md#Examples), they use extension functions made on the Iterable interface. The collection is iterated through in one way or another and the various operations can be made on each element. However, there is another creation in Kotlin that takes a different approach to traversing through a list and applying operations. The name of this creation is a `Sequence`.
### Sequences Vs. Collections
The TLDR version of this is that sequences are used mainly for multi-operation chains and can technically be infinite, while the collection extensions get the job done with less overhead for single operation chains on a finite collection.

To get into a little more detail, a `Sequence` is basically a wrapper for an `Iterator` that provides additional functionality and behaviors. The biggest difference between the two is how they operate and consequentially where they are used.

Iterators evaluate *eagerly*, which in practicality means that in an operation like the following they evaluate every element at every step of a potential chain before proceeding. It also means that they have to store a potential intermediate list as the operations are performed. They also return a list at the end of that iteration:
```kotlin
val list = listOf(1,2,3)
  .filter { println("Filter $it, "); it % 2 == 1 }
  .map { println("Map $it, "); it * 2 }
// Prints: Filter 1, Filter 2, Filter 3, Map 1, Map 3,
```
Because they said it best, here's a snippet directly from the [Kotlin blog][kotlin-blog]:
> Sequences are lazy, so intermediate functions for Sequence processing don’t do any calculations. Instead they return new Sequence that decorates the previous one with new operation. All these computations are evaluated during terminal operation like toList or count.
```kotlin
val list = sequenceOf(1,2,3)
  .filter { println("Filter $it, "); it % 2 == 1 }
  .map { println("Map $it, "); it * 2 }
  .toList()
// Prints: Filter 1, Map 1, Filter 2, Filter 3, Map 3,
```

As far as what this means for you goes, it's probably enough to understand that an iterator function is usually good enough or even better when dealing with small sets of data, while a sequence is generally recommended for large sets of data or when you are performing a set of operations.

Just for fun, here's an example of where a sequence wins in regards to time:
```kotlin
val sequence = generateSequence(1) { it + 1 }.take(5000000)
val list = sequence.toList()
println("Iterable = ${(measureTimeMillis { list.map { it * 2 }.filter { it % 2 == 1 }.sum() }.toDouble() / 1000)}") // prints "Iterable = 2.173"
println("Sequence = ${(measureTimeMillis { sequence.map { it * 2 }.filter { it % 2 == 1 }.sum() }.toDouble() / 1000)}") // prints "Sequence = 0.125"
```
In this case, running this operation chain with a sequence yielded a result about 20 times faster. Despite the fact that the gains are not necessarily this large all the time, a hint added since Kotlin 1.2.70 states that a multiple operation chain on a collection should be changed to a sequence.

There's a much more in depth discussion and explanation of all of this [here on the Kotlin blog][kotlin-blog], and another one particularly regarding speed of operations [here on a Medium article][sequences-speed-article]

[Back To Lap 3: Collection Operators](/operators.md) | [On To Finish Line](/fin.md)
