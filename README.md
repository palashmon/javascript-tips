# Javascript Tips

Useful JavaScript Tips &amp; Tricks

<br>

## Contents

- [Console Table - Display tabular data as a table](#console-table).

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

## Next Tip

Coming soon...
