## `Collection Operators`
To me, this is one of the most exciting parts about Kotlin collections. While it's not just collections that have these, the built in functions for collections give so much added benefit to one of the primary pieces of development. I mean after all, how many times in a day do you create and then transform a collection? I'd bet it's a lot.

For starters, say we just want to alter a property on each element of a Java `List<Animal>` class:
```java
for (Animal animal: animalList) {
  animal.setAdopted = true;
}
```
In Kotlin:
```kotlin
animalList.forEach {
  it.adopted = true
}
```
Now to be clear, this is just an extension function that is adding or condensing functionality. In the `_Collections.kt` file where this `forEach` function is defined, you can see that it's just doing pretty much the same thing as above:
```kotlin
public inline fun <T> Iterable<T>.forEach(action: (T) -> Unit): Unit {
  for (element in this) action(element)
}
```
However, there is a long list of these operators found in the documentation that add so much ease of use. I'll list a few examples here, but I'd encourage you to go and look through the list for yourself just to keep them in the back of your mind. Note that there are different operators available for [`Collection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-collection/index.html) and [`MutableCollection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-collection/index.html).

### Examples
#### Filter
The `.filter` function is a little self explanatory in that it filters a collection by a given predicate (function) which returns a boolean
```kotlin
val animalList = listOf(Dog(true), Cat(true), Lizard()) // constructor initializes adopted field
val filteredResult = animalList.filter { it.getAdopted() }
println("$filteredResult") // prints "[DOG, CAT]"  (overridden toString)
```
#### Partition
The `.partition` function separates a collection into two collections and returns a `Pair` of collections 
```kotlin
val animalList = listOf(Dog(true), Cat(true), Lizard())
val filteredResult = animalList.partition { it.getAdopted() }
println("$filteredResult") // prints "([DOG, CAT], [LIZARD])"
```
#### Map
The `.map` function applies a transformation to each element in the collection and returns the results as a list. This is especially helpful when needing to transform lists of objects that don't have a 1:1 relationship.

I'll also slip in the `.joinToString` operator which creates a string from all the elements in a collection using a supplied `separator`, `prefix`, or `postfix` if desired.
```kotlin
val dogNetworkResponseList = listOf(DogNetworkResponse(false), DogNetworkResponse(true), DogNetworkResponse(true))
val mapResult = dogNetworkResponseList.map { Dog(it.getAdopted()) }
println("${mapResult.joinToString { it.getAdopted().toString() }}") // prints "false, true, true"
```
#### Get Or Null
The `.getOrNull` function handily tries to get the element at a certain index in a list, and if that index is out of bounds it returns `null`.



Again, these are just a few examples of what you can do with the collection operators. Please go check them out in the official docs and play around with them so that you can add these to your toolbelt: [`Collection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-collection/index.html) and [`MutableCollection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-collection/index.html)

[Back To Lap 3](/variance.md) | [On To Lap 5: `Sequences`](/sequences.md)
