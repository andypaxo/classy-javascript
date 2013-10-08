# Classy JavaScript - Scope

## Scope vs. context

Coming from C#, it's possible to get scope and context mixed up due to the rigidity of class definitions. In JavaScript context and scope are independent and distinct.

* **Scope** defines which variables are visible from a given line of code. The scope of a variable is determined by where it is defined in code. JavaScript's scopes are defined at the function level (not the block level like C# or Java)
* **Closures** are closely related to scope. If you're a functional programming guru you won't like me saying this, but you probably don't need to really grasp the difference between scopes and closures.
* **Context** defines which object the `this` variable points at. With a simple function call, the context will be the same object that the function is defined within, just as in C#. However, using `call` or `apply`, the context can be changed to a different object. Beware! This often happens with callbacks, so your `this` object might not be what you expect it to be.

Let's go into a little more depth here...

## Global scope

When a variable is declared outside of any function _or_ when a variable is declared without the `var` keyword, it ends up in the global scope. In the browser (or in Cordova) this is the `window` object.

## Local scope

When a variable is declared in a function, it is in scope _from the point of declaration onwards_. It might seem odd to be able to write a function that calls another function which is declared later when writing a constructor, but take a careful look here...
    
    var Person = function () {
        this.sayName = function () {
            // Here we use this.getName(). It might not look like
            // the function is in scope at this time, but the
            // context (this) is in scope and will have mutated by
            // the time we run this code.  
            console.log('I am ' + this.getName());
        };
        
        this.getName = function () {
            // Likewise, we can use name here, as it will be added
            // to the current scope before this line is run
            return name;
        };
    
        // We cannot, however use the variable 'name' here at this
        // level. Any code here will be evaluated before the
        // variable is created
        
        // Declare a variable in the current scope. Note that
        // it is not added to the context. It is, in effect, a
        // private variable. Don't declare variables down here
        // in real life, though
        var name = 'Spartacus';
    };

new Person().sayName();

## Context, call and apply

We're used to the idea that when we declare a function like this:

	this.doSomething = new function() { ... }

That `doSomething` will always run in the context in which it was declared. That is, that the `this` variable will stay the same. It ain't necessarily so.

Check this out:

    var arthur = {
        name: 'Arthur Dent',
        introduce: function (introducee) {
            console.log('Hi ' + introducee + ' my name is ' + this.name);
        }
    };
    
    var ford = {
        name: 'Ford Prefect'
    };
    
    arthur.introduce.call(ford, 'Trillian');

Yeah, Ford just stole Arthur's function in order to get the first word in. Which is typical of him. Using `Function.prototype.call`, we can replace the context when calling any function by passing our new context as the first argument.

This might seem like a weird thing to do, but jQuery does it all the time... think of using `$(this)` in event handlers. 

`Apply` works the same way, but we can pass an array of parameters rather than the parameters themselves. Handy when we don't know what the parameters are going to be beforehand.   