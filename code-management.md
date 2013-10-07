# Classy JavaScript - Code management

## Functions

## Constructor functions

## Prototypes

Constructor functions are *not* classes. They are also not objects with the properties that they define. This is why we use an object created by the constructor function as the prototype, not the constructor function itself.

We can set the prototype of a newly constructed object directly, or we can use Object.create