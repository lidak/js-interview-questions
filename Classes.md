# Inheritance
1) **Q:** How to make class A a subclass of class B?  
**A:** Use ```extends``` keyword:
    ```
      class A extends B {}
    ```

2) **Q:** What is requirement to subclass'es constructor?  
**A:** If there is a constructor present in the subclass, it needs to first call super() before using "this".

3) **Q:** How ```extends``` word under the hood?  
**A:** It uses prototype inheritance to make parent class a prototype of subclass.

# Statics
1) **Q:** What is class's static method?  
**A:** Static methods are not called on the instances of the class. They can be called on the class itself. They're utility functions usually.

2) **Q:** What is the difference between accessing static methods from another static methods and not-static methods?  
**A:** In order to call a static method within another static method of the same class, you can use the ```this``` keyword.
But you can't do this insight non-static methods. You need to use the class name or by calling the method as a property of the constructor:
    ```
        class StaticMethodCall {
          constructor() {
            console.log(StaticMethodCall.staticMethod());
            // 'static method has been called.'

            console.log(this.constructor.staticMethod());
            // 'static method has been called.'
          }

          static staticMethod() {
            return 'static method has been called.';
          }
        }
    ```

# Methods overwriting/super
1) **Q:** What would be the result of following code last line function call?  
    ```
      class A {
        constructor(name) {
          this.name = name;
        }
    
        sayHello() {
          console.log(this.name);
        }
      }
    
      class B extends A {
        sayHello() {
          alert(this.name)
        }
      }
    
      const b = new B('Alex');
    
      b.sayHello();
    ```
    
    **A:** alert with Alex string would be shown. B class's own sayHello method overwrites it's parent class method.

2) **Q:** How to modify B class's method to call it's parent method before alerting name?  
**A:** Use ```super``` keyword
    ```
      class B extends A {
          sayHello() {
            super.sayHello()
            alert(this.name)
          }
        }
    ```