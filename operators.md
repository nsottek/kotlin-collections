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


[Back To Lap 3](/variance.md) | [On To Lap 5: `Sequences`](/sequences.md)
