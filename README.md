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

The quick explanation of how this works is that the function call `doSomething()` executes and 
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

However, the expression-based defaulting technique is a quite clever use of the short-circuiting nature of boolean operators.

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
If `foo` doesn’t exist (or is some falsy value), then the second clause assigns the empty object to foo.

It’s really another way of saying:

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


