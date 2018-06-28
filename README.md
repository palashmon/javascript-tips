# Javascript Tips

Useful JavaScript Tips &amp; Tricks

<br>

## Contents

- [Console Table - Display tabular data as a table](#console-table).
- [Console Log With Variable Name](#console-log-with-variable-name).

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

## Next Tip

Coming soon...
