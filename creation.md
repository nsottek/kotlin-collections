## `Creating Collections`

### Java Land
In Java, this is what declaring a collection would look like:
```java
ArrayList<Int> numbers =  new ArrayList<>()
```
Note that Java requires the manual specification of the type for that collection. That is because the `ArrayList` signature takes a generic type that needs to be defined:
```java
public ArrayList(Collection <? extends E> c) { ... }
```
That generic type `E` is what needs to be specified explicitly. Additionally, most collections have to be instantiated before items can be added to them, though there are some convenience methods exist that make creation easier like so:
```java
ArrayList<Integer> numbers = new ArrayList<>( Arrays.asList(1, 2, 3, 4) );
```
However this is still fairly verbose when compared to the same in Kotlin, which is consistent with comparing other aspects of these languages.

### Kotlin-topia
While you can also declare the type of list element on creation in Kotlin, the type can also be inferred based on the contents of the initialized collection. For example:
```kotlin
val list = listOf(1, 2) // List<Int> is implied here
```
In this case, it has been inferred that the collection is being instantiated with an element type of `Int`. There's another interesting difference to call out here though. You might be tempted to ask what type would be inferred in the following scenario:
```kotlin
val list = listOf(1, "Two")
```
Obviously this can't be inferred as having an element type of `String` or `Int`. In you're familiar with Java, you might be tempted to say `Object` since this is the superclass of everything, and you'd basically be right. In Kotlin there is a class called `Any`, and it is extended by all the things. So in that last example, this would be inferred as a `List<Any>`.

There are still cases where you might need to define the type that the collection will be instantiated with, such as when there are no initial values from which a type can be inferred:
```kotlin
val emptyList: List<Int> = emptyList()
val emptyListOf = listOf<Int>() // both of these values would be an empty collection of Int elements
```
#### Global Factory Methods
Note that there is not an implementation specified in the creation of these collections. That is part of a bigger movement in Kotlin to keep abstracting the things that can be abstracted. The following list of methods is a more expansive list of these factory methods that go along with the `listOf()` call I've shown so far:
```kotlin
val list = listOf(1, 2)
val mutableList = mutableListOf(1)
val set = setOf(1)
val mutableSet = mutableSetOf(1)
val map = mapOf(1 to "First", 2 to "Second")
val mutableMap = mutableMapOf(1 to "First", 2 to "Second")
val array = arrayOf(1, 2, 3)
```
I will note that there are technically other implementation specific methods for using certain collection types, but it is generally encouraged to use these factory methods for creating a collection. The factory methods are in fact interfaces with underlying implementation that suit each case. There are various reasons for this, and here are a few that stick out to me:
1. If the underlying implementation needs to change, you should be guaranteed that the contract of the interface will be upheld.
2. There's generally not much reason to have to specify the use of a certain collection, and generally I've seen developers default to the more common collection types when a more efficient one might be available. It's time and efficiency gained for other things if this is something that can be done by the compiler instead.
3. Readability. The compact sense of `val list = listOf(1, 2, 3)` is a wonderful thing

The documentation has this to say on the subject:
> Currently, the listOf method is implemented using an array list, but in future more memory-efficient fully immutable collection types could be returned that exploit the fact that they know they can't change.

That's a great segue into our next topic: `Mutability`. Follow me to lap two as we break down the concept of mutability in Kotlin collections.

[Back To Starting Line](/README.md) | [On To Lap 2: `Mutability`](/creation.md)
