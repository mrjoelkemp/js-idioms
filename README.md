JavaScript Idioms
=========

A collaborative collection of some interesting (not necessarily specific to) JavaScript idioms.

Have another to share? Pull request it in. Hopefully, programmers of all skill levels can benefit.

---

### Branching with inline assignment

```javascript
if (foo = doSomething()) {
}
```

The way this works is that the function call `doSomething()` executes and
its returned value gets stored in `foo`.
The value of `foo` is then evaluated for truthiness.

This is really just a more concise way of saying:

```javascript
foo = doSomething();

if (foo) {
}
```

### Exploiting Boolean Operators for Function Execution

```javascript
callback && callback();
```

This is a shorter way of saying:

```javascript
if (callback) {
 callback();
}
```

Alternatively, you can one-line it to be more concise:

```javascript
if (callback) callback();
```

However, the expression-based defaulting technique uses the short-circuiting nature of boolean operators.

Here it is again:

```javascript
callback && callback();
```

If `callback` doesn’t exist, then the condition is immediately `false`
(since boolean and expects both clauses to be true – hence, the first clause must
be true to bother evaluating the second one) and moves on without evaluating the second clause.

If `callback` does exist, however, then the second clause is
evaluated – executing the callback function.

### Expression-based Variable Defaulting

```javascript
foo || (foo = {});
```

Similar to the previous idiom, this one also takes advantage of short circuiting.
If `foo` doesn’t exist (or is some falsy value), then the second clause assigns the empty object to `foo`.

It’s another way of saying:

```javascript
foo = foo || {};
```

which are both shorter ways of saying:

```javascript
if (! foo) {
  foo = {};
}
```

### Appending an array element using its length

```javascript
var a = [];
a[a.length] = 'foo';
```

This works because `a.length` evaluates to 0 initially (it's an empty array) and
so ‘foo’ gets stored/appended in `a[0]`. Another iteration of this idea could be:

```javascript
var a = [];
a[a.length] = 'foo';
a[a.length] = 'boo';
```

After the first assignment, `a.length` evaluates to 1, so ‘boo’ gets stored/appended in `a[1]`.

Alternatively, you could just use the native `push` function.

```javascript
var a = [];
a.push('foo');
```


### Conditionals with Binary NOT

*Taken from visionmedia/superagent*

```javascript
 this.url += ~this.url.indexOf('?')
      ? '&' + query
      : '?' + query;
```

The NOT Binary operator converts a given integer, N, into the -(N+1) value.
For example, the ~-1 gives us -(-1+1), which is -0, of just 0.

The code above checks if there's a `?` in the url string. If there is **no**
question mark, `indexOf` returns -1, the ~ of which is 0 (falsy in this
ternary operation) which means that the question mark will be added.

If the question mark was found, then the binary NOT of it (wherever it is
within the string) would be non-zero, adding the ampersand to the query string.

### Removing duplicates from an array

```javascript
myarray.filter(function(elem, idx) {
    return myarray.indexOf(elem) === idx;
});
```

The gist of this is that a duplicate will have a previous copy that occurs earlier in the array. As such,
that copy will have an index not equal to that of the current element.

Example: `[1, 2, 1]`

For the first 1, the `indexOf` the first occurrence of 1 is the same as the index of the current 1 – zero.
For the second 1 (the copy), the `indexOf` the first occurrence of 1 is 0, not 2 (the current index of the duplicate).
Since the indices are not equal, the duplicate is not included in the filtered set.

It's still an O(n^2) algorithm, but pretty succint.