./[curric](/curric)/[kotlin](/curric/kotlin)/[basics](/curric/kotlin/basics)/[Type-Hierarchy](/curric/kotlin/basics/typehier)/
# Kotlin Type Hierarchy
Every Type in Kotlin has 2 forms: A non-nullable form and a nullable form (denoted with a `?`)
![](https://i.imgur.com/fgO0TDn.png)
However
![](https://i.imgur.com/Q5G2EGU.png)
This means that if a parameter is created as an instance of `Int`, you are still able to pass in an `Int?` as `Int?` is a "super" type of `Int`. Therefore all Nullable Types are a **super** type of the Non-Nullable Type