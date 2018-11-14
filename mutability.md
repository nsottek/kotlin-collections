## `Mutability`
As a concept, mutability refers to the likelihood that something will be changed. With Kotlin collections, this concept is very evident. The reasons behind this are pretty straightforward. Per the documentation, ` Precise control over exactly when collections can be edited is useful for eliminating bugs, and for designing good APIs.` For ease of conversation, I'll deal mostly with the list collection, but know that this concept applies to (almost) all of the other collections as well.

### Immutable Collections
Collections that are created as immutable cannot be modified after their initialization. For example:
```kotlin
val numbers = listOf(1, 2, 3)
numbers.add(4) // this line will not compile
```
The collection in this example conforms to the `List` interface, which as mentioned in the previous section is different from the Java `List` interface in that it is immutable. Items in these immutable collections can still be accessed, like with the indexing operator `numbers[0]` or convenience methods like `numbers.first()`, but the values they hold cannot be mutated. 

### Mutable Collections
Like I showed in [`Lap 1`](/creation.md#standard-library-factory-methods), there are separate methods for creating immutable vs. mutable collections. The following would be for a mutable list:
```kotlin
val numbers = mutableListOf(1, 2, 3)
numbers.add(4)
println(numbers) // prints "[1, 2, 3, 4]"
```
The collection in this example conforms to the `MutableList` interface, which implements the `List` interface and is more like the `List` interface found in Java. For these mutable collections, you would be able to call any of the standard mutating functions like `add`, `remove`, `set`, and `clear`.

### Can I Get One From The Other?
Now, say you want to get an immutable list from this mutable list so that you could pass it along to somewhere that should not have the right to mutate its values. There is a simple convenience method called `.toList()` that *copies* the values into a **new**, immutable list object. The same concept also applies in reverse, as in going from an immutable list to a mutable list only requires calling `.toMutableList()`. To demonstrate:
```kotlin
val numbers = mutableListOf(1, 2, 3)
val immutableNumbers = numbers.toList() // Copies values into a new immutable list

numbers.add(4)
// immutableNumbers.add(4) // does not compile

println(numbers) // prints "[1, 2, 3, 4]"
println(immutableNumbers) // prints "[1, 2, 3]"

val mutableNumbers = immutableNumbers.toMutableList() // Copies values into a new mutable list
mutableNumbers.clear()
mutableNumbers.add(0)

println(mutableNumbers) // prints "[0]"
println(numbers) // prints "[1, 2, 3, 4]"
println(immutableNumbers) // prints "[1, 2, 3]"
```
### Read Only Reference
There is another important distinction to make, and that is that there is a `difference between a read-only view of a mutable collection, and an actually immutable collection (Kotlin Docs)`. I think it makes the most sense when seen in action:
```kotlin
val mutableNumbers = mutableListOf(1, 2, 3)
val numbersReadOnlyView: List<Int> = mutableNumbers // Obtains a read-only reference

println(mutableNumbers) // prints "[1, 2, 3]"

mutableNumbers.add(4)
// numbersReadOnlyView.add(5) // does not compile

println(numbersReadOnlyView) // prints "[1, 2, 3, 4]"
```
As you can see, despite `numbersReadOnlyView` being immutable, that value itself is referencing the mutable list whose values can change. So while calling `.add(5)` does not compile, the `.add(4)` call to the original list changes the values that the read only val is referencing.

[Back To Lap 1: `Creating Collections`](/creation.md) | [On To Lap 3: `Collection Operators`](/operators.md)
