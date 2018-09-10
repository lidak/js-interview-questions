# Functions

#### Declaration vs Expression
1) **Q:** What would be results of following examples run:
    ```
    function foo(){
        function bar() {
            return 3;
        }
        return bar();
        function bar() {
            return 8;
        }
    }
    alert(foo());
    ```

    **A:** JS will alert 8 because both bar-declarations got hoisted.

    ```
    function foo(){
        return bar();
        var bar = function() {
            return 3;
        };
        var bar = function() {
            return 8;
        };
    }
    alert(foo());
    ```
    **A:** None of bar-expressions hoists so we'll have 'bar is not a function' type error.
2) **Q:** Why to use function-expressions?

    **A:** Function expression can be assigned conditionally or reassigned.
    Function expression can be anonimous.
3) **Q:** What would be result of the following code execution:
    ```
    bar();
    function foo() {
      function bar() {
        console.log(2);
      }
    }
    ```
    **A:** RefferenceError: world is not defined. bar function is declared insight another function scope.
    And would not be available from out of it despite the fact it's function declaration.
#### Arrow functions
  1) **Q:** What is an arrow function?
      **A:** It's an anonimous function that changes way ```this``` binds and has following structure:
      ```
      () => {};
      ```
  2) **Q:** How to access all the arguments in arrow function like we do in normal function using ```arguments```?
      **A:** Use rest operator like this:
      ```
      let a = (...args) => {console.log(args.length)};
      a(1,2,3); // 3
      ```
  3) **Q:** Describe ```this``` behavior insight arrow function
    **A:** In arrow function ```this``` is bound to context where it was created. That helps to avoid confusion around it in callbacks and nested functions.

#### IIFE(Imediately invoked function expression)
1) **Q:** How to make sure variables of third party code doesn't conflict with your code?
  **A:** Use IIFE

2) **Q:** How to make sure variables from your code affect IIFE code? Consider code bellow.
    ```
    var a = 2;

    (function() {
        console.log(a);
    })()
    ```

    **A:** Pass it as a parameter

    ```
    var a = 2;

    (function(a) {
        console.log(a);
    })(a)
    ```
3) **Q:** Why example bellow does not work as an IIFE?
    ```
    function foo() {}();
    ```
    **A:** The function above is declaration. To make it function expression we have to remove it's name and wrap it with paranthesis.
    By wrapping the anonymous function inside of parentheses, the JavaScript parser knows to treat the anonymous function as a function expression instead of a function declaration:
    ```
    (function(){})()
    ```

#### Constructor checking
1) **Q:** How to access constructor function from it's instance?
    **A:** Every instance of class has ```constructor``` implicit reference to it.

2) **Q:** How to check whether object is a direct instance of a constructor?
    **A:**
    ```
    function Constructor() {};
    var instance = new Constructor();

    instance.constructor === Constructor // true;
    ```
#### new.target
1) **Q:** How to check whether function was called with using ```new``` operator?
    **A:**
    ```
    function Foo() {
      if (!new.target) throw 'Foo() must be called with new';
    }
    ```

2) **Q:** What ```new.target``` of arrow functions reffers to?
  **A:** In arrow functions it reffers to surrounding function's ```new.target```
#### Callbacks
1) **Q:** What are callbacks?
    **A:** Callback is a function that is passed as an argument to another function to be called insighd it later.
2) **Q:** What is the problem and solution of a 'callback hell'?
    **A:** Callback hell is an issue that emerges from usage of asyncronous javascript or javascript with lots of callbacks.
    As usually this ends up in pyramid-shaped code that is hard to understand and maintain.
    In case of syncronous code it can be solved by modularization or splitting it down to smaller function.
    If we deal with asyncronous code we can use
    - async/await;
    - promises;
    - generators;

    to solve the callback hell issue.

3) **Q:** Describe your favourite way of handling/avoiding callback hell. Please explaing it.
#### Generators
1) **Q:** What's the difference beetween the regular function and generator?
    **A:** * Generator function can yield control back to the caller at any point.
           * When you call a generator, it doesn’t run right away. Instead, you get back an iterator. The function runs as you call the iterator’s next method.

2) **Q:** Where would you use ```yield*```
**A:** It's used in places where we want to call generator insight the other generator

3) **Q:** What happens when we use ```return``` instead of generator's last ```yield``` ?
**A:** It would behave similarly when performing the iteration by hand, using ```next```. On the side, when using a defined data consumer such as ```for-of``` or destructuring, the returned value is ignored.
#### Pseudo 'arguments' array
 1) **Q:** Make an ES5 function that returns sum of all passed arguments
    **A:**
    ```
    function sum() {
      return Array.prototype.reduce.call(arguments, function(a, b) {
        return a + b;
      }, 0);
    }
    ```
 2) **Q:** What is ```arguments```?
 **A:** ```arguments``` is an array-like object, but it doesn't have any array properties except ```length```
 3) **Q:** How to access all the arguments from within arrow function?
 **A:** Use ```rest``` operator;




# Classes