# Function, Method and Procedure

Three distinct concepts used interchangeably especially in JavaScript world. I might be brave to say but this famous indistinction very well span across entire programming community \(of course except for Functional Programmers\). And there is a good reason for that. Programmers often don't have necessary academic background required to understand abstract concept. Even if they do, there is a void between academic world and its application in real world.

To best put it words, function, methods and procedures are series of related instruction grouped together to execute within a larger program. This is the common part. The distinction lies in their formal definition:

> A **Function** will always have an input\(s\) and one or more output\(s\). **Procedure**, on the other hand, may or may not have input or output. It is simply set of commands that are to be executed in order.
>
> **Method** is basically an OOP concept which literally means any **Function** or **Procedure** defined on an object. They will always have implicit context \(famously known as `this` pointer\) associated with them.

## Examples

### Function

```js
// Exactly one input and one output
function square(x) {
    return x * x;
}

// Take two arguments and return one output
function addition(a, b) {
    return a + b;
}
```

### Procedure

```js
// Takes no input and returns no output
function sayHello() {
    console.log('Hello there!');
}

// Takes one input and returns no output
function displayMyName(name) {
    alert('Your name is: ' + name);
}

// Takes no input but returns one output
function getRandomNumber() {
    return Math.random();
}
```

### Method

```js
class Person {
    constructor(name) {
        this.name = name;
    }

    // getName() is the method of Person class
    getName() {
        // Method always has implicit `this` pointer set to calling object (known as context).
        return this.name;
    }
}

const p = new Person();

// Method will always be called upon some object.
// Here method is implicitly associated with object p.
p.getName();

// Method is explicitly called with object p using `.call()` method
Person.prototype.getName.call(p);
```

If you are familiar with JavaScript, then above examples should be clear. You will notice that **no matter what, you will always use JavaScript functions to create function, procedure and method**. **Programming languages in their attempt to keep their syntax \(more accurately grammar\) simple and concise do not make distinction between these concepts**.

There are some programming languages that make this distinction between function and procedure more explicit. Syntax to create them is different. **Pascal **is one language I am aware of. I don't recall any other modern language doing this distinction.

## Notes on Method

Remember I earlier mentioned that methods always have `this` pointer associated with them. Well, any Python programmer will raise his finger. In Python, when you create class, you don't have `this` pointer. Instead every method is made available `self` reference as a first parameter. It looks like this:

```py
class TestClass:
    a = 10

    ## Here self refers to instance object
    def func(self):
        print('Hello')
```

However, the idea of `context` still prevails. It could be `this` pointer or `self` reference. It is just convenience and syntactic sugar a language has chosen to simplify developer's life.

Going further, one might ask - **what about static methods defined on a class?** We can do that in almost any OOP language including JavaScript? Should they be called **static functions**. Simply put, there is no definite answer to that. But I personally choose to call them method. The reason being, though they don't have context of the object as such, they are privileged and can still access special fields \(private fields\) of that class and thus in some way they still have context.

## Functions and Procedure

> When it comes to procedure, you can quite surely say that they read some global state or modify \(mutate is the fancy word for modification\) it. If you are not doing any of that, then it probably means your procedure is empty.

Whereas functions may or may not depend upon global state. It is considered bad practice for a function to access global state. Why that is so is another concept in programming known as **Purity**. It entirely is a separate topic and should be covered in later notes.

Also, I mentioned that functions always return one or more value\(s\). In most languages, they return one value. Some lanauges like **Go **allows you to return multiple values. Some languages don't support returning multiple values as part of their syntax but support it via concept of **Tuple**. JavaScript doesn't have tuple. Python has it. In JavaScript, we fake returning multiple values via array or map.

In mathematical world, functions will always return exactly one output. This branch of math is **lamda calculus**. **I can further conclude that function not just returns one output, but it also expects exactly one input**. You might wonder if there is any use at all. But rest assured, it is very valid proven approach and entire functional programming \(FP\) is based on this. FP will someday be the future of programming that was envisioned by Alan Turing.

## Uses

All this theory, is it of any use? In your daily programming, maybe very little. But understanding abstract concept of function is very vital to understand other abstract concepts.

## Read Further

\[TODO\]: Links to be added

Functions in depth

Lambda Calculus

Function arity

