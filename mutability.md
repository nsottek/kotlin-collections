## `Mutability`
As a concept, mutability refers to the likelihood that something will be changed. With Kotlin collections, this concept is very evident. The reasons behind this are pretty straightforward. Per the documentation, ` Precise control over exactly when collections can be edited is useful for eliminating bugs, and for designing good APIs.`

### Immutable Collections
Collections that are created as immutable cannot be modified after their initialization. For example:
```kotlin
val numbers = listOf("a", "b", "c")
numbers.add("d") // this line will not compile
```
There are specific methods like 


[Back To Lap 1: `Creating Collections`](/creation.md) | [On To Lap 3: `Variance`](/variance.md)
