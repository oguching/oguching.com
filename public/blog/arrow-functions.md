Arrow function in JavaScript is not new anymore but I have been reluctant to use them until quite recently.

## What are arrow functions?
Arrow functions allow you to write more concise JavaScript code. In most cases arrow functions can be used in place of the regular `function` keyword in JavaScript.

**Syntax**  
`identifier => expression`  

Let's look at an example. In ES5 you may write an `add` function like this

```JavaScript
  ES5 
  "use strict"
  
  var add = function (a, b) {
    return a + b
  }
```

Here we are using a function literal with two parameters that sums up the parameters entered and assigns the value to the add variable. How would we write this with arrow functions? Well, let me show you

```JavaScript
  const add = (a, b) => a + b
```

That's it! Let's break it down. We are using `const` to declare our `add` variable. You can use `var` or `let` if you like. One obvious difference is the `function` keyword is missing. We replaced it with the arrow function (`=>`) and moved it to the right of our parameter list, the return expression follows after the arrow function sans the `return` keyword. Arrow functions automatically return so you don't have to include the return keyword.

I read that the parentheses around parameters can be omitted if there's only one parameter. While that is true and works, it's a good idea to keep the parens even if there's one parameter. It helps make your code more readable in general and avoid tricksy errors. Personally, I don't like too many rules and break some on purpose. I don't use semi-colons for example and think it's generally okay to go without, my code looks nicer without those hideous things but that's me. You decide if it's worth the trouble for you.

Let's look at another example. This one I took from [hacks.mozilla.org](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)

```JavaScript
  // ES5
  "use strict"

  var total = values.reduce(
    function (a, b) {
      return a + b
    }, 0
  )
```

What's happening here is that we are adding all the supposedly numbers array (it could well be a string array) that is `values` using the Array.reduce() method and assigning the result to `total`. What does this piece of code look like when we use arrow functions? It looks like this

```JavaScript
  const total = values.reduce((a, b) => a + b, 0)
```

Again, does the same thing and fits nicely in one line, plus it really looks nice to my eye. Honestly I don't know why I didn't adopt arrow functions much earlier.

Let's look at one more example. Remember when I said you don't need to explicitly use the `return` statement? Well... let's just see this example.

```JavaScript
  // ES5
  "use strict"

  [1, 2, 3, 4].map(function (num) {
    var multiplier = 2 + num
    return num * multiplier
  })

  // -> [3, 8, 15, 24]
```

If you still write ES5 it's a good idea to use the strict mode. It will help you write better code. So [map](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/map) is an Array method that creates a new array after operations on each element in the calling array. 

With the above code we add 2 the first element in the array, then multiply the result with the first element (1) then store the result in a new array at the first index location. We do same for each element in the array then return the result. Here's how it looks with array functions

```JavaScript
  [1, 2, 3, 4].map((num) => {
    let multiplier = 2 + num
    return num * multiplier
  })
```

As you can see we added the `return` statement. Turns out, if you use arrow functions with a block body, you need to use the `return` statement. This might also be a good time to state that when using arrow functions to create plain objects, always wrap the objects in parentheses. For example do

```JavaScript
  const toy = puppies.map((puppies) => ({})) // Good boy
```

But do not do this

```JavaScript
  const toy = puppies.map((puppies) => {}) // No boy, no.
```

**More caveats**
* Arrow functions are anonymous. 
* Arrow functions do not have their own `this` value.


If you keep these in mind you should be fine using arrow functions. Are you sold yet?

## Conclusions
Arrow functions in JavaScript allows you to write more concise readable code. It does away with the `function` keyword, replacing it with a `=>` symbol and for most cases you don't need an explicit `return` statement. 

Even if you're not going to use it yourself, you'll read code that has it and quite frankly it reads better than having functions everywhere. Plus think of all the less typing you'll have to do now. `=>` ist gud.

## Further explorations
* [Hacks.mozilla blog](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)  
* [PonyFoo](https://ponyfoo.com/articles/es6-arrow-functions-in-depth)  
* [Babel repl](https://babeljs.io/repl/)  
* [CoffeeScript Fat Arrow](http://coffeescript.org/#literals)