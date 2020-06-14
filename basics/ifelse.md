./[curric](/curric)/[basics](/curric/basics)/[if-else-if-else](/curric/basics/ifelse)/
# If... Else If... Else
Sometimes it is helpful to execute a block of statements only if a certain boolean condition evaluates true. In this case, `if` statements can be used.
```java
if(condition) {
    // do something
}
```
If you need an alternative case for if the condition is false, use `else`:
```java
if(condition) {
    // do something
} else {
    // do something else
}
```
Lastly, sometimes it is helpful to chain different conditions together so that only one block is executed:
```java
if(condition) {
    // do something
} else if(anotherCondition) {
    // do something else
} else if(anotherNotherCondition) {
    // a third thing
} else {
    // a last option
}
```
Remember that any block will only be executed if its condition is true and if all the conditions above it were false. If they are all false, then the `else` block is run. 