---

layout: post
title: Flake it till you make it
subtitle: Excerpt from Soulshaping by Jeff Brown
bigimg: /img/path.jpg

## tags: [books, test]

Under what circumstances should we step off a path? When is it essential that we finish what we start? If I bought a bag of peanuts and had an allergic reaction, no one would fault me if I threw it out. If I ended a relationship with a woman who hit me, no one would say that I had a commitment problem. But if I walk away from a seemingly secure route because my soul has other ideas, I am a flake?

- **let**: This is a new keyword available to declare variables. The awesomeness of this keyword is that it does not do any kind of [hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting).
- **const**: This is another new keyword that has been added to the specification. It allows us to create true constants in JavaScript.
- **Block scoping**: Essentially the ability to to create scopes using curly braces.

## let

Using this new property is pretty straight forward

```javascript
'use strict';
let variable = 'I am a variable';
console.log(`Variable: ${variable}`)
// Output: Variable: I am a variable
```

The example above shows how to use this new keyword. Not too different from **var** so far. I already mentioned that this new property does not get any kind of hoisting. But what does that really mean?
Hoisting is basically the ability to reference properties that have not been already declared when the JavaScript interpreter registers a specific section of code.

An example will probably help to clarify

```javascript
'use strict';
console.log(`The total amount is: ${ amount }`);
var amount = 50;

// Output: The total amount is 50
```

If you are coming from an object-oriented language you will likely find this atypical. We are showing a variable before it has been declared. This is something that a compiler would simply not accept. However JavaScript is an interpreted language and this is totally legal. The reason behind this is a feature present in JavaScript called [hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting). This is the process where the interpreter moves all the variables and function declarations to the top of your file (Not in a physical way of course).

So let's see what happens if we replace **var** with **let** in the last example

```javascript
'use strict';
console.log(`The total amount is: ${ amount }`);
let amount = 50;

// Output: ReferenceError: amount is not defined
```

In essence variables declared with **let** cannot be hoisted. Hence a property declared using **let** cannot be used before its declaration. This is an excellent new feature that I strongly recommend start using because it will help reduce the amount of errors in our code. *Now life is not perfect so take a look [here](https://caniuse.com/#search=let) to see browsers support before you decide to use it.*

> Browsers might return different messages for the example above. Firefox 59 returns: **"ReferenceError: can't access lexical declaration amount before initialization"** which some might found deceiving

## const

As I stated before this keyword gives us the ability declare constants in JavaScript. By definition the value of a constant cannot be changed once it has been initialized. So this is great for values that must not change during the flow of a JavaScript code

Let's see an example

```javascript
const PI = 3.14159;
console.log(`PI is equal to: ${PI}`);
// Output: PI is equal to: 3.14159
```

Now let's rewrite the example above and attempt to change the value during runtime

```javascript
const PI = 3.14159;
// Attempting to change its value
PI = 4;
console.log(`PI is equal to: ${PI}`);
// Output: Uncaught TypeError: Assignment to constant variable
```

As we can see changing the value of a constant is ilegal and we will get an error if we ever try to do that. It should not come as a suprise because *const* is a shortcut for *constant*. *Take a look at the browser support [here](https://caniuse.com/#search=const) before you decide to use this property*

## Block Scope

Another feature that many programmers have found complicated in JavaScript is scope. Scope is the accessibility of variables, functions and objects in a specific section of your code during runtime. Until ES6 the only real scope existing in the language was the function scope. Meaning that variables declared inside of a function where limited to that scope. But other statements like *for*, *while*, *if*, *switch*, etc do not have their own scope unlike object-oriented languages. So a lot of developers with that background might have a difficult time to understand this.

This can be a real problem and result in a lot of bugs if not handled correctly. Workarounds where created for this problem but all of them are far from simple and most developers did not really use them (In my experience)

Let's clarify with some examples

### Global scope

```javascript
'use strict';
value name = 'Salvador';
console.log('My name is ' + name);
// Output: My name is Salvador

function showName() {
  // The name varialbe is accessible here and everywhere else.
  console.log('My name is ' + name);
  // Changes made to the varialbe will persist outside this function
  name = 'Matt';
}
console.log('My name is ' + name);
// Output: My name is Matt
```

The example above shows how the global scope works. Basically a variable created at the global scope can be accessed at any section (Other scopes included) and changes made to this variable persist.

### Local Scope

```javascript
'use strict';
var showName = function {
  // The variable name has been declared and initialized inside of function
  // Since functions are the only elements that have a local scope, this 
  // new property is not accessible from the global scope
  var name = 'Salvador';
  console.log('My name is ' + name);
  // Output: My name is Salvador
};
// Global scope: No name variable exists here
```

Let's see a final example where we can see all the scopes in a typical JavaScript file

```javascript
'use strict';
// Global scope
function firstFunction () {
  // Local scope #1
  function secondFunction () {
    // Local scope #2
  }
}

// Global scope
function thirdFunction () {
  // Local scope #3
}
// Global scope
```

Having a good understanding of scopes makes it easier to avoid overriding a variable or assuming we are working on a different scope.

So what has changed in ES6 you might be wondering? Well essentially curly braces now create their own scope. Let's see that in action

```javascript
'use strict';
let userId = 1;
// Unlikely you'll ever do this in a real application but 
// just follow me on this
{
  let userId = 2;
}
console.log(`User Id: { userId }`);
// Output: User Id: 1
```

So we declared a variable called userId at the global scope. The using curly braces we created a second scope and a new variable called userId was created. But since in ES6 this creates a new scope the variable at the global scope is not being overriden but a second variable in a local scope has been created.

Let's probe with another example that the curly braces have their own scope

```javascript
'use strict';
{
  let userId = 1;
}
console.log(`User Id: {userId}`);
// Output: Uncaught ReferenceError: productId is not defined
```

So the userId variable we created inside of the curly braces is not accessible from the global scope. This is a totally familiar behavior if once again you have an object-oriented language background.

Scopes and variables can be tricky thought. Let's see one example of this

```javascript
'use strict';
function updateUserId() {
  userId = 2;
}
let userId = null;
updateUserId();
console.log(`User Id {userId}`);
// Output: User Id: 2
```

The really interesting thing here is that a function can make use of an variable that has not been declared yet. The interpreter will not have a problem with this. The only requirement is that variables must be defined before they are being accessed.

All the previous new features are great additions to the JavaScript specification. Now the only thing is to be able to use them depending on the browsers our projects need to support. In general as community I think we should push users into upgrading their browsers to the most recent versions so we all get the benefits of this.

-Happy coding
