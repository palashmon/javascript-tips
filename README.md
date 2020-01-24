# Javascript Tips

Useful JavaScript Tips &amp; Tricks

<br>

## Contents

- [Console Table - Display tabular data as a table](#console-table).
- [Console Log With Variable Name](#console-log-with-variable-name).
- [Short code to create array of `n` length from `0` to `n-1`](#short-code-to-create-array).
- [Conditionally Spread Object](#conditionally-spread-object).
- [Conditionally adding properties inside Object](#Conditionally-adding-properties-inside-object).
- [Type Checking JavaScript Files](#Type-checking-javaScript-files)
- [Easily trace execution time of Promises](#easily-trace-execution-time-of-promises)
- [Check if an array with a length is not just empty slots](#check-if-an-array-with-a-length-is-not-just-empty-slots)

<br>

## Console Table

You might have come across a situation like this where you have to wade through a sea of array of objects just to check a particular object key value in the array for debugging purpose maybe. Something like this:

![img1](/assets/images/jstip1.png)

... and then you tried to guess where that object could be and kept opening and closing each object one by one, something like this:

![img2](/assets/images/jstip2.png)

In such cases, you can easily review the data in nice table format using `console.table` like:

```js
// You have an array of object
var data = [{...},{...},{...},{...},{...},{...}];

// Just pass it to console.table
console.table( data );
```

and after that you will see something like this in your console:

![img3](/assets/images/jstip3.png)

which now you can easily scroll and check for object key value that you have been looking for.

MDN Web Docs: [Console.table()](https://developer.mozilla.org/en-US/docs/Web/API/Console/table)

<br>

## Console Log With Variable Name

There might have been a situation where you `console.log` some variables in app like:

```js
console.log(id, name, completed, submitted);
```

and then check in console for results on page refresh and find something like:

```
23 "palash" true false
```

Now at first look you might have some confusion like "_Is `completed` true or false here?_" You just check the app/IDE again and confirm based on position of variables inside `console.log` that `completed` is actually true here and `submitted` variable is false. But you can just wrap the curly brackets `{}` around your `console.log` arguments to see the variable names along with the value in a easy comprehensible format, taking the advantage of ES6 shorthand syntax like:

```js
console.log({ id, name, completed, submitted });
```

and now in your browser console you will see something like:

![img4](/assets/images/jstip4.png)

Now you can easily say that `completed` is indeed `true` here.

Reference: [Wes Bos's 2016 Tweet](https://twitter.com/wesbos/status/798579690575462400)

## Short Code To Create Array

Sometimes we might need to create an array of `n` length like `[0, 1, 2, ..., n-1]`. We can do this easily using ES6 [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) like:

```js
[...Array(n).keys()];
```

This is a general version. If you need an array of length `10`, then you can set it like:

```js
[...Array(10).keys()];
// Result => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Brief explanation

1.  `Array(10)` create an empty array of length `10` like `[,,,...]` where value of any index from 0-9 is `undefined`.
2.  `Array(10).keys()` this returns a new **Array Iterator** object that contains the keys for each index in the array.

    ```js
    var array1 = Array(3);
    var iterator = array1.keys();

    for (let key of iterator) {
      console.log(key); // expected output: 0 1 2
    }
    ```

3.  `[...Array(10).keys()]` this creates a new, shallow-copied `Array` instance from `Array(10).keys()` iterable object.

### Bonus Trick

If you want the array to start from `1` and end with `n` here like `[1, 2, 3, ..., n]` instead of `[0, 1, 2, ..., n-1]`, then you can do like this:

```js
[...Array(10)].map((v, i) => ++i);
// Result => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

## Conditionally Spread Object

We can conditionally spread an object - because `{...false}` (and undefined/null/etc) is just `{}`.

```js
let person;
const defaultAddress = {
    street: '4253  Rebecca Street',
    city: 'Chicago',
    state: 'Illinois',
    country: 'US'
}

// In case, person object has not been set yet then person is `undefined`
const shipping = {
 	...defaultAddress,
	...person.address
}
// and the above code gives an error:
// Uncaught TypeError: Cannot read property 'address' of undefined

// We can conditionally spread the person object like:
const shipping = {
 	...defaultAddress,
	...(person && person.address)   // this will result in {...false} == {}
}

// and we will not get any type error incase person object has not been set yet
```

## Conditionally adding properties inside Object

We can return two different objects with or without certain property, based on a condition using the spread operator. 

```js
// A boolean `emailIncluded` determines whether the property `email` is added to the return object
const getUser = (emailIncluded) => {
  return {
    name: 'Wes',
    surname: 'Bos',
    ...(emailIncluded && { email : 'wes@bos.com' })
  }
}

// Get user details with email
const user = getUser(true);
console.log(user);
// Returns:
// {name: "Wes", surname: "Bos", email: "wes@bos.com"}

// Get user details without email
const userWithoutEmail = getUser(false);
console.log(userWithoutEmail);
// Returns:
// {name: "Wes", surname: "Bos"}
```

The spread operator for object does nothing if its operand is an empty object 

```js
{a: 1, ...{}}
// Returns:
// {a: 1}
```

## Type Checking JavaScript Files

Want TypeScript's type checking for regular JavaScript?

Opt in via comment: // @ts-check  
Via CLI: tsc file.js --allowJs --checkJs --noEmit  
Via config: "checkJs": true  

If types can't be inferred, use JSDoc annotations.
Learn more: [Link](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html)  

![img2](https://pbs.twimg.com/media/EN-6ARpUcAI41Md?format=jpg&name=small)  

## Easily trace execution time of Promises

Easily trace execution time of Promises with a combo of `await` & `finally`

```js
const delay = require("delay");

trace("How long?", async () => {
  await delay(500);
});

// Adapted from https://github.com/apollographql/apollo-server/blob/d5015f4ea00cadb2a74b09956344e6f65c084629/packages/apollo-datasource-rest/src/RESTDataSource.ts#L281
async function trace(label, fn) {
  if (process && process.env && process.env.NODE_ENV === "development") {
    const startTime = Date.now();
    try {
      return await fn();
    } finally {
      const duration = Date.now() - startTime;
      console.log(`${label} (${duration}ms)`);
    }
  } else {
    return fn();
  }
}
```

# Check if an array with a length is not just empty slots

We can determine if an array with a length is not just empty slots, using array `filter()` method. The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```js

// Make an array with 4 empty slots
Array(4)
=> (4) [empty × 4]

// Check this array length
Array(4).length
=> 4

// But does all of the array slots have a valid value
// 0 here means that all of the slots of this array are empty
Array(4).filter(Boolean).length
=> 0

// To verify we can create an array with two empty slots and 2 valid slots
Array(undefined, undefined, 3, 5)
=> (4) [undefined, undefined, 3, 5]

// Check this array length
Array(undefined, undefined, 3, 5).length
=> 4

// But does all of the array slots have a valid value
// 2 here means that only two slots have a valid value in this array
Array(undefined, undefined, 3, 5).filter(Boolean).length
=> 2
```

## Next Tip

Coming soon...
