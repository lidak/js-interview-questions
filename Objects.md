# Objects

## Prototype

### Constructor

### \__proto\_\_
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
3) **Q:**
     **A:**

## Object literal

## Operations with object

### Object creation
### Defining properties
### Properties descriptors
### Object merging
### Properties iteration
### Copying
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
