./[curric](/curric)/[basics](/curric/basics)/[Syntax](/curric/basics/syntax)/
# Syntax
When reading Java code, there are a few types of syntax elements you will run across. 

## Statement

A statement can invoke an action, declare a variable, or do other nifty things you're soon to learn about. It always ends in a semicolon. 
```java
int i = 1;
i++;
lukesCar.detachMuffler(); // still salty about that
```
"Wait, what's that? The double slash followed by your words?"
\- you, probably
## Comment
Whenever you feel like including blurbs in your code, just add `//` and everything after it on that line is not executed!
If a comment is rather long and lasting a few lines, you can surround it with `/*` and `*/`, called a block comment.
```java
// the next line declares an integer i and sets it to 1
int i = 1; // maybe we should set it to 2 instead? 
// too late, now i is 1
// bet
i = 2;
/*
 I have some concerns with the above code:
 complexity
 over use of comments
 unused variable i
 */
```
## Blocks
Blocks of some form or other, varying from control structures to class definitions, group sets of statements for semantic and functional purposes with curly braces, `{` and `}`.