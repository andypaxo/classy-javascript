# Classy JavaScript - Code management

JavaScript can emulate inheritance and classes as we are used to them from c#. It's clunky but it works. Most of the time, however, it isn't required. There is no type safety in JavaScript, and there are many other ways for objects to share functionality. See _JavaScript: The Good Parts_, chapter 5 for a few ideas.

## Constructor functions

These are the typical way of adding data to a newly created object. They can also be used to add functionality, but at the cost of some overhead when creating objects.

    var Dwelling = function (material) {
        this.material = material;
        this.description = 'A house';
    };

## Prototypes

We can use prototypes to add behaviour to our "class". The prototype is also used for inheritance

    Dwelling.prototype.describe = function () {
        console.log(this.description + ' made of ' + this.material);
    };

We can then use this class-type object to define a subclass-type object, thusly:

    var Apartment = function (material) {
        this.material = material;
        this.description = 'An apartment';
    };

    // Use an instance, not the constructor function itself!
    Apartment.prototype = new Dwelling();

    Apartment.prototype.findEntrance = function () {
        console.log('Look on the second floor');
    };

    new Dwelling('wood').describe(); // A house made of wood
    new Apartment('brick').describe(); // An apartment made of brick
    new Apartment().findEntrance(); // Look on the second floor

Constructor functions are *not* classes. They are also not objects with the properties that they define. This is why we use an object created by the constructor function as the prototype, not the constructor function itself.

We can also set the prototype of a newly constructed object directly, or we can use Object.create
