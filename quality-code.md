# Classy JavaScript - Quality code

JavaScript is very free and easy as to what it will tolerate as acceptable code. It's also very flexible and there are a great many different ways to accomplish any task (just look at the number of ways you can write a "class"). There's no widely agreed on coding standard, and JavaScript's culture owes much more to cut-copy-paste than it does to red-green-refactor.

All of this adds up to great potential for a huge mess. We'll have to be vigilant to maintain standards. Fortunately, the nice people of the internet have made us a plethora of tools to aid us.

## Code documentation

In the C# world, we're used to writing (mostly) self-documenting code. Rigid class definitions and static typing mean that we can get away with just making sure that our names are good and letting Visual Studio project navigation do the rest.

We don't have that level of rigidity in JavaScript, so we might just have to resort to documenting our code. (At the very least, noting what each function is expecting for parameters). After a cursory glance around the internet, YUIDoc looks like the most promising candidate for this job. If you've used JavaDoc before, it will feel quite familiar.  

## Unit testing

QUnit is probably the most popular unit testing tool and so is worth mentioning. There. I mentioned it.

Cordova creates Jasmine tests with new projects. Jasmine is a BDD testing tool and should feel familiar from our "context spec" / RhinoMocks tests. Check this on up out:

    describe("A suite", function() {
        it("contains spec with an expectation", function() {
            expect(true).toBe(true);
        });
    });

Jasmine has facilities for creating test suites, mocks, expectations and all the usual good stuff that we've come to expect from testing frameworks. It can also be run server-side, but we should look into how we get the output into a suitable form for CI.

## UI / subcutaneous testing

If any of you have used QUnit before, you might be familiar with the idea of manipulating the DOM as part of tests. Jasmine doesn't allow this, but given our previous attempts with UI based testing, that probably isn't a bad thing.

We can, if we structure our code carefully, do testing *just under* the UI. That is we can write integration tests with several real services working in unison on a view model. That would be a good idea. 

## JSLint

JSLint catches a lot of easy to make JavaScript mistakes and will make our code much more consistent and easier to read. You'll hate it.

You'll hate it for two reasons:

 1. It's really pedantic and will keep pointing out tiny little inconsequential style inconsistencies that really don't need to be fixed right now
 2. Andy likes consistent code, so he'll keep prodding you fix them

(As an aside, look at the commit comments in the JSLint Git repository. Do the absolute opposite of that and you'll be fine).
 