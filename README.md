JavaScript Idioms
=========

Collection of some interesting, not always specific to, JavaScript idioms. 

The goal is to expose different ways of expressing fundamental thoughts.

Have another to share? Pull request it in.

---

### Branching with Inline assignment

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

Again:

```javascript
callback && callback();
```

If `callback` doesn’t exist, then the condition is immediately false 
(since boolean and/&& expects both clauses to be true – hence, the first clause must 
be true to bother evaluating the second one) and moves on without evaluating the second clause.

If `callback` does exist, however, then the second clause is 
evaluated – executing the callback function.


