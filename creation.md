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
In this case, it has been inferred that the collection is being instantiated with an element type of `Int`. There are still cases where you need to define the type that the collection will be instantiated with, such as when there are no initial values from which a type can be inferred:
```kotlin
val emptyList: List<Int> = emptyList()
val emptyListOf = listOf<Int>()
```

Note that there is not an implementation specified in the creation of these collections. Follow me to lap two as we break down the global factory methods for collections.

[Back To Starting Line](/README.md) | [On To Lap 2: Factory Methods] (/creation.md)
