# Statement and expression

A question that will never be asked in any technical discussion - What is the difference between statement and expression? So why we should bother learning about this. Before I tell you why, it is imperative that we understand these two distinct concepts. Even JavaScript, as a language, makes distinction between statement and expression. For this article, we will use JavaScript as our context unless explicitly stated.

## What is an expression?

Any line of code that produces some value is expression. Following all are expressions:

```js
// Adding x to 10 and producing new value
x + 10        // if x is 5 then it produces 15.

// Calling a function square(x: number) such that it always returns x * x
square(2)    // ---> 4
```

In short, evaluation of some part of code \(it could be block, function call, one/many lines of code\) should produce value.

## What is a statement?

Statement is any line of code that performs some action. Following are statements:

```js
// Calling a method log on console object
console.log('Hello world');

// all loops and if blocks are statements
if (x > 10) { /* do something */ } else { /* something else */ }
```

For the `if` statement, no value is produced. We cannot do:

```js
let y = if (x > 10) { return 25; } else { return false }    // ERROR
```

However, I can do something similar using expression with the help of ternary operator:

```js
let y = x > 10 ? 25 : false;    // Expression
```

## Expression vs Statement

**If expressions are constructs that stand for values, then typically statements are constructs that control the execution of the program.** All expressions are statements but not vice a versa. As [Dr. Axel](http://2ality.com/2012/09/expressions-vs-statements.html) puts it:

> A program is basically a sequence of statements. Wherever JavaScript expects a statement, you can also write an expression. Such a statement is called an **expression statement**. The reverse does not hold: you cannot write a statement where JavaScript expects an expression. For example, an `if` statement cannot become the argument of a function.

Expressions are composable and reducible. Composable means smaller expressions can combine in various ways to generate bigger expressions \(does it ring a bell with functional programming\). Reducible means complex expressions can be simplified and optimized to yield better performance either by programmer, compiler or runtime engine.

## Consequences

The distinction between expression and statement is subtle yet important. Being composable and reducible is the core principle of functional programming. Expressions are preciously that. You will notice that imperative or OOP style of programming have statements as their major ingredient whereas functional programming style favors expressions. More functional the language is, more the number of expressions. 

In fact, a language like Haskell takes it to the extreme. Each and everything in Haskell is expression. There are no statements. Even `if` construct is an expression in Haskell. That is why if you are using `if-else` expression in Haskell then it is mandatory to write `else` part and it should return same type of value that `if` part returns.

Using statements almost means you are doing some sort of control flow and as such are the major sources of side effects. Statements can only be combined vertically in a sense that they are meant to be executed in sequence.

Expressions are the other hand can be combined horizontally \(meaning composable\). This leads to an amazing property of referential transparency. When we write pure functions, then such functions mostly contain expressions and thus we can **memoize** result of expensive function or replace it with an optimized version, 

It can even execute expressions in parallel on multi-threaded CPU since expressions need not be combined **vertically **like statements. This can all happen at compiler level without programmer having to explicitly write constructs to achive parallel programming. Or else, imagine having to write thread, handle thread safety, using semaphors, etc...

## What about declaration?

Is it expression or statement? Well it more hybrid than being something specific. Declaration, at least, is statement. And you can add expression to declaration to combine assignment into it. For example:

```js
let x = 2 * 8;    // A declaration statement
```

In simple terms, **declarations are constructs that introduce identifiers** \(variables, constants\) in the system to simplify programming.

