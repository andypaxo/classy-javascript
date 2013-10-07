# Classy JavaScript - Scope

## Scope vs. context

Coming from C#, it's possible to get scope and context mixed up due to the rigidity of class definitions. In JavaScript context and scope are independant and distinct.

* **Scope** defines which variables are visible from a given line of code. The scope of a variable is determined by where it is defined in code. JavaScript's scopes are defined at the function level (not the block level like C# or Java)
* **Closures** are closely related to scope. If you're a functional programming guru you won't like me saying this, but you probably don't need to really grasp the difference between scopes and closures.
* **Context** defines which object the `this` variable points at. With a simple function call, the context will be the same object that the function is defined within, just as in C#. However, using `call` or `apply`, the context can be changed to a different object. Beware! This often happens with callbacks, so your `this` object might not be what you expect it to be.

Let's go into a little more depth here...

## Global scope


## Local scope


## Context, call and apply

