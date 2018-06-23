---
layout: post
title: Abstract Value Operations
subtitle: The rules that govern convertion of value types to primitives
gh-badge: [star, fork, follow]
share-img: /img/javascript.png
tags: [javascript, abstract-operations, toString, ToNumber, ToBoolean]
---
### Abstract Value Operations
I have found that a lot of developers out there continually get confused about the result of converting certain value types to primitives. There is in fact a set of rules on how value types and specific values are converted to the different primitives. All this magic happens internally in *abstract operations* (``ToString``, `ToNumber`, ``TooBoolean`` and ``ToPrimitive``) that contain the rules for the conversion.

#### ``ToString``
This abstract operation handles the conversion of any non-string value. Primitives have the next stringification rules

``null`` --> ``'null'``

``undefuned`` --> ``'undefined'``

``true`` --> ``'true'``

``numbers`` --> A string representation of the number value. i.e  ``4`` --> ``'4'``

``objects`` --> Unless specified something, the internal class will be returned. i.e ``[object Object]``

``arrays`` --> They are special. Their ``toString()`` function stringifies each value and concatenates all of them with a ``,`` between each

Let's see a couple examples of this
``` javascript
var array = [1, 2, 3];
// Explicit coercion
array.toString(); // Output: 1, 2, 3

var number = 250;
// Explicit coercion
number.toString(); // Output: '250'

var boolean = true;
// Explicit coercion
boolean.toString(); // Output: 'true'
```
Please note that I added the comment *Explicit coercion* to each entry. This is just because I want to emphasize the coercion type being applied. **It does not matter if coercion is explicit or implicit. When applied on non-string values and used in a ``string`` context the ``toString()`` function will always be called.**

#### ``ToNumber``
This abstract operation is defined for any non-number value that is required to be a number. Primitives have the next conversion rules

``true`` --> ``1``

``false`` --> ``0``

``undefined`` --> ``NaN``

``null`` --> ``0`` // Curious ha?

``string`` --> It works as expected. Please note that if the conversion fails then ``NaN`` is returned

``objects``

Objects (and arrays) are first converted to their primitive value equivalent. And if the primitive value is not already a number then the ``ToNumber`` function is applied. 

Now the process to convert an object to primitive value goes like this: the ``ToPrimitive`` abstract operation is called and it will try to retrieve the value by checking for the existence of the ``valueOf`` function. If the function exists and it does return a primitive value then that value is returned and ``toNumber`` applies the rules explained above. But if the ``valueOf`` function is not defined and the ``toString()`` function it is then ``toString()`` will provide the primitive value. If both functions are not available or for some reason do not return a primitive value a ``TypeError`` exception is thrown.


#### ``ToBoolean``

This abstract operation is by far the one that most confusion generates. I believe this is because most developers get started with object-oriented languages and they expect a similar behavior in JavaScript.

So first things first, yes JavaScript does have the ``true`` and `false` keywords and they behave exactly as you would expect and more importantly: any value being coerced to `boolean` will result in either `true` or `false`.

##### Falsy values
This concept is essentially how we describe a list of values that when coerced to `boolean` result in false. This is the falsy values list
- `undefined`
- `null`
- `false`
- `+0`
- `-0`
- `NaN`
- `''`

Not too long, ha? From this we can assume that if the value we are trying to coerce to `boolean` is not in this list. Then it will result in `true` meaning it is a truthy value.

No examples as I think I have been really clear.

##### Truthy values
These are basically all the values that when coerced to `boolean` result in `true`. Yes I know what you are thinking "*Just give me the list*". But if you are paying attention you already figured it out. **A truthy value is any value that does not belong to the falsy list.**

Let the list of examples begin!
``` javascript
// This is me making you a big favor
var falseString = Boolean('false'); // Output: true 
var zeroString = Boolean('0'); // Output: true
var whiteSpaceString = Boolean(' '); // Output: true
```
So let's examine what is going in on in the examples above. In the first example we are coercing the string `'false'` to `boolean`. Now I know that in a lot of compiled languages this results in `false`, however not in JavaScript. Do you see the `'false'` value in the falsy list? Me neither. 

How about the `zeroString` variable? Well in that example we are coercing the string `'0'` to `boolean` but remember. The only string that results in `false` is the empty string. So result is as expected `true`

At this point I'd say you already figured out the last one. Yes a white space is not part of the list of the falsy values. So results is `true`

What an interesting set of rules, he? A good understanding of how JavaScript works behind the scenes makes things clearer and it is a great way to avoid some of the issues that most developers face when not having this knowledge.

Thanks for reading and have a happy coding!