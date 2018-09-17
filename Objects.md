# Objects

## Prototype

### Constructor

### \_\_proto__
1) **Q:** What does __proto__ point at in case of object creatied using object/function/array literal?
    **A:** It points at ```Object/Function/Array.prototype``` object.

2) **Q:** What is the best way to get prototype of an object?
    **A:** Actually ```__proto__``` is the wrong answer. It considered deprecated and can be not supported by some browsers. So use ```Object.getPrototypeOf()``` or ```obj.constructor.prototype``` instead.

3) **Q:** What is going to be when we try to set ```__proto__``` to some not-object value? Let's say 1?
    **A:** Nothing. ```__proto__``` would remain unchnged. It can be set to null or object values only.


### Prototypal inheritance
1) **Q:** Object bellow has no methods. Why we can call ```hasOwnProperty``` and can't ```someCustomMethod``` method on it?

    ```
      var a = {};
      a.hasOwnProperty('b') // false;
      a.someCustomMethod() // TypeError: a.someCustomMethod is not a function
    ```

    **A:** ```Object.prototype``` has method ```hasOwnProperty``` and object ```a``` can access it through prototype chain.
2) **Q:** Given constructor function ```Animal```, it's instance ```rabbit``` and their prototype. Describe how they are bound?
  **A:** ```rabbit``` like every other instance has implicit ```constructor``` link (in our case it points to ```Animal``` function).
  And ```Animal``` like every other function has implicit ```prototype``` link. If we want to access prototype object from ```rabbit``` we can do it:

    ```
    rabbit.constructor.prototype
    ```
3) **Q:** List all the possible ways for extending the prototype chain
     **A:**
     - New initialization;
     - Object.create;
     - Object.setPrototypeOf;
     - \_\_proto__

## Object literal
1) **Q:** How to subscribe to object's property change? Let's say we want to log to console whenever ```obj.prop``` changes.
    **A:** Use setter:
    ```
      const hell = {
         _a: 1,
         set a(newValue) {
           console.log(`_a is to be set to ${newValue}`);
           this._a = newValue
         }
      }
      hell.a = 2;
    ```
2) **Q:** How to set prototype of object literal?
    **A:** Use \_\_proto__ prop:
    ```
      const obj = {
        name: 'Petro',
        __proto__: {
          printName: function() {
            console.log(this.name);
          }
        }
      }

      obj.printName() // Petro
    ```

3) **Q:** How to call object literal's prototype method from within it's own method?
    **A:** Use ```super``` keyword
    ```
      var calc = {
        numbers: null,
        sumElements () {
          return this.numbers.reduce(function(a, b) {
            return a + b;
          });
        }
      };
      var numbers = {
        __proto__: calc,
        numbers: [4, 6, 7],
        sumElements() {
          // Verify if numbers is not null or empty
          if (this.numbers == null || this.numbers.length === 0) {
            return 0;
          }
          return super.sumElements();
        }
      };
      numbers.sumElements(); // => 17
    ```
## Operations with object

### Object creation
1) **Q:** List all the possible ways to create an object in JS?
    **A:**
    ```
      const myObj = new Object();
      const anotherObject = {};

      const somePrototype = {doSomething: () => {console.log('Doing something')}}
      const oneMoreObj = Object.create(somePrototype);
    ```
 2) **Q:** What is the difference between two approaches to create numeber variable bellow?
    ```
      const num = 2;
      const num1 = new Object(2)
    ```
    **A:** Second assignment would create ```Number``` instance object wrapper for number value
 3)
### Defining properties
### Properties descriptors
### Object merging
### Properties iteration
1) **Q:** how to loop through own object's properties?
    **A:**
    ```
      for(let propName in object) {
        if(object.hasOwnProperty(propName)) {
          // some code goes here
        }
      }
    ```

    ```
      Object.keys(object).forEach((propName) => {
        // some code goes here
      })
    ```
### Copying
1) **Q:** How to create a deep copy of an object in JS?
    **A:** You can use
    ```
      JSON.parse(JSON.stringify(a))
    ```
    or make recursive function to iterate through object's own properites and set em to new object.
    ```Object.assign``` is wrong answer because it makes shallow copy.
### Freezing
1) **Q:** How to make object immutable using vanilla JS?
  **A:** Use ```Object.freeze``` method;

2) **Q:** What is the result of following code execution?
    ```
    var employee = {
      name: "Mayank",
      designation: "Developer",
      address: {
        street: "Rohini",
        city: "Delhi"
      }
    };

    Object.freeze(employee);

    employee.name = "Dummy"; // fails silently in non-strict mode
    employee.address.city = "Noida"; // attributes of child object can be modified

    console.log(employee.address.city) // Output: "Noida"
    ```
    **A:** Freeze affects first level properties/methods only. Nested objects can be changed after freeze. So ```employee.address.city``` would be changed.

3) **Q:** What is the difference between ```Object.freeze``` and ```Object.seal``` methods?
    **A:** The ```Object.seal()``` method seals an object, preventing new properties from being added to it and marking all existing properties as non-configurable. Values of present properties can still be changed as long as they are writable.
