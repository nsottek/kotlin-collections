## `Variance`
First off, I'll copy and paste the Wikipedia definition of variance so that we're on the same page.
> Variance refers to how subtyping between more complex types relates to subtyping between their components. For instance, if the type Cat is a subtype of Animal, then an expression of type Cat can be used wherever an expression of type Animal is used. How should a list of Cats relate to a list of Animals?
### Types of Variance
Generally speaking, the types of variance relationships are `covariant` or `contravariant`, `bivariant`, and `invariant`.
#### Covariant
If a complex type is `covariant`, that means that it retains the relationship between its components. Let's use the example of having `Animal` and `Cat` where `Cat` is a subclass of `Animal`. In this case, if there is a `List<Animal>` and a `List<Cat>` then the `List<Cat>` would be a subclass of `List<Animal>`, since by definition the complex type of `List` maintains the pre-existing relationship between it's components.
#### Contravariant
If a complex type is `contravariant`, that means that reverses the relationship between its components. With the same example where `Cat` is a subclass of `Animal`, a `List<Animal>` would actually be a subclass of `List<Cat>`. From what I could find, this is not very commonly seen in OOP languages but is still out there.
#### Bivariant
If a complex type is `bivariant`, this means that it is both `covariant` and `contravariant`. Again, this is not commonly found in OOP languages. For conversation's sake, this would mean that `List<Animal>` and `List<Cat>` would both be a subclass of the other.
#### Invariant
If a complex type is `invariant`, it does not retain any relationship between its components. This is the case with Java collections. For example, even though `Integer` is a subclass of `Number` we see the following:
```java
List<Integer> integerList = new ArrayList<>();
List<Number> numberList = integerList; // does not compile
```
A `List<Integer>` cannot be assigned to a `List<Number>` because `List`s are invariant (and mutable for that matter).
### Variance in Kotlin
For collections in Kotlin, **read-only** collections are `covariant`. This applies to both collections created as immutable and the read-only view of a mutable collection. So for example, you can do this in Kotlin:
```kotlin
val catList: MutableList<Cat> = mutableListOf(Cat(), Cat(), Cat())
val animalList: List<Animal> = catList
```
But not this:
```kotlin
val catList: MutableList<Cat> = mutableListOf(Cat(), Cat(), Cat())
val mutableAnimalList: MutableList<Animal> = catList // does not compile
mutableAnimalList.add(Dog()) // contents could change
```
This makes sense because you wouldn't want to have the case where you would be trying to add a `Dog` to your `catList`.


[Back To Lap 2: `Mutability`](/mutability.md) | [On To Lap 4: `Collection Operators`](/operators.md)
