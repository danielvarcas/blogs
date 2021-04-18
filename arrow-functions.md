# ES6 Arrow Function Syntax Explained Simply

Photo by <a href="https://unsplash.com/@flowforfrank?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Ferenc Almasi</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  

## Introduction
This is a JavaScript arrow function:
```
const getUserIds = users => users.map(user => user.id)
```
If your response to the above code is, "What, what?!", then read on! Even if you do understand what's going on, you may still pick up a thing or two along the way.

Some initial questions you may have:
- What is it doing?!
- What is it returning (if anything)?
- What does the arrow mean?
- What is `users` doing there?

In this article, I want to go over the basics of arrow functions to help new JavaScript developers understand what is *actually* going on here.

## A quick bit of history

ES6 was the 6th Edition of JavaScript released in 2015. It is also known as "ECMAScript 6" or "EMCAScript2015". ES6 was a major revision of JavaScript, and introduced new syntax to help developers write complex code in a simpler form.

One of these new additions was arrow function syntax. Arrow function syntax (or just "arrow syntax") provides a different method of writing functions, in a way that is often shorter and mostly quicker to write and comprehend once you've grasped how the syntax works.

## "Normal" functions vs arrow functions

Here is a simple **function declaration** in basic JavaScript:
```
function times10(number) {
  return number * 10;
}
```
Here is the same thing as an **arrow function** using ES6 arrow syntax:
```
const times10 = number => number * 10;
```

Let's pick out the main, visible differences in the arrow function:
- There are no curly braces (`{}`)
-  There are no parentheses (or "brackets") around the function parameter (i.e. `= user =>`)
- Arguably, the syntax is a bit more *streamlined*.

Note that I use the word "streamlined", and not "better" or "simpler".

## How is this useful?
Perhaps you're not convinced that the use of arrow syntax in the above example is providing anything much more useful than the "normal" way of writing functions. In this case, I'd tend to agree. However, arrow functions begin to show their use in more complex scenarios.

Take the below function, which gets ids from an array of user data:

```
getUserIds(users) {
  return users.map(function(user) {
    return user.id;
  }
}
```

Using arrow syntax, we can choose to write this function as follows:
```
const getUserIds = users => users.map(user => user.id);
```
In some ways, you may find the arrow function more readable and probably quicker write too. Try writing each function in a code editor and see how they compare.

Now, let's break down what is happening in the arrow function's single line of code: 
- We are **defining a variable** called `getUserIds`. 
- The **value** of `getUserIds` is **a function definition**.
- *That* function takes an argument named `users`. 
- The function uses a JavaScript array function called `map()` to iterate over each item in the `users` array and **return a new array** containing only the user ids.
- The function **returns the array that was returned** by the map() function.

All on one line. 

## How did we get here?

Arrow function syntax is flexible, and we could have written this function in a few different ways, including being more verbose with our syntax. 

For example, each of these functions when called would map over the `users` array and return an array of user ids:

```
// ✔️
const getUserIds1 = (users) => {
  return users.map(user => user.id);
}

// ✔️
const getUserIds2 = users => {
  return users.map(user => user.id);
}

// ✔️
const getUserIds3 = users => users.map(user => user.id)
```

In the second example, we were able to remove the parentheses from around the `users` parameter, and it works exactly the same.

Why do this? Arguably: for simplicity, though it is entirely optional. Note that **this only works** for functions with a **single parameter**.

In the third example we stripped the syntax down further, removing the braces (`{}`) and the `return` keyword. This is called **implicit return**.

### Multiple parameters
If your function has multiple parameters (takes multiple arguments), you must use parentheses:

❌ Will throw a syntax error
```
const getUserIds4 = users, prefix => {
  return users.map(user => prefix + user.id);
};
```

✔️ This is fine
```
const getUserIds5 = (users, prefix) {
  return users.map(user => prefix + user.id);
};
```

#### Argument destructuring
You must however always use parentheses when using argument destructuring:

❌ Will throw a syntax error
```
const user = { id: 1, name: "Daniel" }
const getName = { name } => name;
```

✔️ This is fine
```
const user = { id: 1, name: "Daniel" }
const getName = ({ name }) => name;
```


### Implicit return
Arrow functions without braces will return the last value returned within it's own scope by default. Note that you should *not* use the `return` keyword when writing an arrow function without braces.

Here are some examples of returning (or not) from arrow functions:

Here is our `users` data:
```
const users = [{id: 1, name: "Aaron"}, {id: 2, name: "Maya"}]
```

❌ Using `return` without braces
```
const getUserIds6 = (users) => return users.map(user => user.id)
                                   ^^^^^^

Uncaught SyntaxError: Unexpected token 'return'
```

✔️ Implicit return
```
const getUserIds7 = (users) => users.map(user => user.id)

getUserIds7(users)

// [1, 2]
```

✔️ Explicit return
```
const getUserIds8 = (users) => {
  return users.map(user => user.id);
}

getUserIds8(users)

// [1, 2]
```
✔️ Explicitly returning nothing (or `undefined`, to be precise)
```
const getUserIds9 = (users) => {
  users.map(user => user.id);
}

getUserIds9(users)

// undefined
```

### Anonymous functions
We can also use arrow syntax to write anonymous functions. I won't go in-depth on anonymous functions here, but this is what they look like in regular and arrow syntax:

Anonymous function declaration:
```
function(x, y) { 
  return x + y;
}
```

Anonymous function expression (implicit return):
```
function(x, y) { x + y }
```

Anonymous arrow functions:
```
(x, y) => x + y;
// Returns x plus y

(x) => x * 100;
// Returns x times 100

x => x
// Returns x

x => {
  return x;
}
// Returns x

const z = 99;
() => z + 1;
// Returns 100;
```

## Ok, but what does the arrow mean?!
The arrow is characters which form syntax which Node or the browser will recognise, just like `===` or `.` or `+`. 

It says: "and now I'm going to tell you what this function does".

A nice way to think about it **semantically** is picturing the arrow as the conveyer belt which moves the arguments through the function.

```
const add = (a, b) => a + b;
// Take these things, (a,b), and move them through 
// in this direction => into the function, leaving 
// the result on the other side.
```

## Some caveats
Arrow functions are not that different from regular functions. Most of time, you can use them interchangeably without fear of consequence.

However, there are a few technical points you should be aware of when using arrow functions.

### No function hoisting

Functions written using the `function` keyword are "hoisted" at runtime. In simple terms, this means the engine running your code (i.e. Node) will take these functions and store them in memory before executing the rest of your code.

✔️ So you can do this:

```
multiply(5, 2)
// 10

function multiply(x, y) {
  return x * y;
}
```
We've written our code in a way where we're calling `multiply()`  before defining what `multiply()` is. 

But because we've used the `function` keyword, at runtime `multiply()` will **hoisted**; it will be read and stored in memory (*defined*) before the line `multiply(5, 2)` is executed.

❌ But you can't do this:
```
multiply(5, 2) // TypeError: multiply is not a function

const multiply = (x, y) => {
  return x * y;
}
```
Because we've used arrow syntax, `multiply()` has not been hoisted. So when the runtime engine gets to `multiply(5, 2)`, it sees that `multiply()` is not defined at this point in the execution and throws an error.

### No `this`
Arrow functions do not have access to `this`. This is perhaps best explained with examples.

✔️ Using a normal function to access `this`:
```
const myObject1 = {
  x: 10,
  getX: function () {
    return this.x;
  }
};

console.log(myObject1.getX());
// 10
```

❌ Using an arrow function to access `this`:
```
const myObject2 = {
  x: 10,
  getX: () => this.x
};

console.log(myObject2.getX());
// TypeError: Cannot read property 'x' of undefined
```

### Other caveats
This article is to help you understand the basics of arrow syntax, but it's helpful to be *aware* (even if you don't understand in detail) that there are some other technical differences with arrow functions. MDN Web Docs has a good [rundown of all the differences](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), if you are interested in further research.

## Are arrow functions better?

Not necessarily. Arrow function syntax provides developers with a tool for writing code in a different way, often with the benefits of code that is easier to read and write.

When ES6 was still fancy and new, arrow functions were seen by some as the "new" way of writing JavaScript functions. Bootcamps and online tutorials would sometimes teach arrow functions by default, and often still do.

But these days, I'm seeing a trend towards bringing it back to the `function` keyword. Kent C. Dodds, a well-renowned React expert, posted [an article](https://kentcdodds.com/blog/function-forms) about how he uses different function forms for different purposes, which makes for interesting reading.

## In Conclusion

ES6 arrow function syntax provides a useful way to write more streamlined code which is often more readable. Code readability is important for helping others to understand your code. Likewise, it's important to be able to read others' code well yourself. So regardless of how you like to write functions, it is good to be able to understand different syntaxes when you encounter them.

I hope this article has been useful for those of you new to writing JavaScript code. If you have an questions, comments, suggestions, or indeed corrections, please let me know in the comments below. I would love to hear your thoughts, whether this article was helpful, and any constructive criticism.

Please feel free to follow me here and on Twitter ([@dan_j_v](https://twitter.com/dan_j_v)).