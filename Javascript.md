# Javascript Questions

1. What is Variable Hoisting?

   It is a Javascript Mechanism where variables and function declarations are moved to the top of their scope before code execution. Also this mechanism moves only declarations and not initialization.

   ```js
   // Example 1
   console.log(name); // error: name is undefined.
   var name = "javascript";

   // Example 2
   function hoist() {
     a = 20;
     var b = 10;
   }

   hoist();
   console.log(a); // 20
   console.log(b); // ReferenceError: b is not defined
   ```

   The above code snippet will be interpreted by Javascript before execution like below

   ```js
   // Example 1
   var name;
   console.log(name);
   name = "javascript";

   // Example 2
   var a;
   hoist();
   function hoist() {
     var b;
     a = 20;
     b = 10;
   }
   console.log(a);
   console.log(b);
   ```

2. What is Function Hoisting?

    JavaScript functions can be loosely classified as the following:

    1. Function declarations
    2. Function expressions

    _Function declarations_

    ```js
    hoisted(); // Output: "This function has been hoisted."

    function hoisted() {
    console.log('This function has been hoisted.');
    };
    ```

    _Function expressions_

    ```js
    expression(); //Output: "TypeError: expression is not a function

    var expression = function() {
    console.log('Will this work?');
    };
    ```

   *Order of precedence*

   1. Variable assignment takes precedence over Function declaration
   2. Function declarations takes precedence over Variable declaratoin

      _Variable assignment over function declaration_

      ```js
      var double = 22;

      function double(num) {
        return num * 2;
      }

      console.log(typeof double); // Output: number
      ```

      _Function declarations takes precedence over Variable declaratoin_

      ```js
      var double;
      function double(num) {
        return num * 2;
      }

      console.log(typeof double); // Output: function
      ```

3. What is Class Hoisting?

    JavaScript class can be loosely classified as the following:

    1. Class declarations
    2. Class expressions

    _Class declarations_

    ```js
    var Frodo = new Hobbit();
    Frodo.height = 100;
    Frodo.weight = 300;
    console.log(Frodo); // Output: ReferenceError: Hobbit is not defined

    class Hobbit {
        constructor(height, weight) {
            this.height = height;
            this.weight = weight;
        }
    }

    //has to be
    class Hobbit {
        constructor(height, weight) {
            this.height = height;
            this.weight = weight;
        }
    }

    var Frodo = new Hobbit();
    Frodo.height = 100;
    Frodo.weight = 300;
    console.log(Frodo); // Output: { height: 100, weight: 300 }
    ```

    _Class expressions_

    ```js
    var Square = new Polygon();
    Square.height = 10;
    Square.width = 10;
    console.log(Square); // Output: TypeError: Polygon is not a constructor


    var Polygon = class Polygon { //named class
        constructor(height, width) {
            this.height = height;
            this.width = width;
        }
    };
    //has to be
    var Polygon = class Polygon {
        constructor(height, width) {
            this.height = height;
            this.width = width;
        }
    };

    var Square = new Polygon();
    Square.height = 10;
    Square.width = 10;
    console.log(Square);
    ```

4. What is a Closure?

    A closure is the combination of a function and the lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables. The closure has three scope chains

    1. Own scope where variables defined between its curly brackets
    2. Outer function’s variables
    3. Global variables Let's take an example of closure concept,

    ```js
    function Welcome(name){
        var greetingInfo = function(message){
            console.log(message+' '+name);
        }
        return greetingInfo;
    }

    var myFunction = Welcome('John');
    myFunction('Welcome '); //Output: Welcome John
    myFunction('Hello Mr.'); //output: Hello Mr.John
    ```
    As per the above code, the inner function(greetingInfo) has access to the variables in the outer function scope(Welcome) even after the outer function has returned.

5. What is Function Currying?

    Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. Currying is named after a mathematician Haskell Curry. By applying currying, a n-ary function turns it into a unary function. Let's take an example of n-ary function and how it turns into a currying function

    ```js
    const multiArgFunction = (a, b, c) => a + b + c;
    const curryUnaryFunction = a => b => c => a + b + c;
    curryUnaryFunction (1); // returns a function: b => c =>  1 + b + c
    curryUnaryFunction (1) (2); // returns a function: c => 3 + c
    curryUnaryFunction (1) (2) (3); // returns the number 6
    ```
    Curried functions are great to improve code reusability and functional composition.

6. What is a callback hell?

    Callback Hell is an anti-pattern with multiple nested callbacks which makes code hard to read and debug when dealing with asynchronous logic. The callback hell looks like below,

    ```js
    async1(function(){
        async2(function(){
            async3(function(){
                async4(function(){
                    ....
                });
            });
        });
    });
    ```
    Callback hell can be avoided using `Promise`.

7. What is a Promise?

    A promise is an object that may produce a single value some time in the future with either a resolved value or a reason that it’s not resolved(for example, network error). It will be in one of the 3 possible states: fulfilled, rejected, or pending.

    ```js
      const promise = new Promise(function(resolve, reject) {
      // promise description
    })
    ```

    The usage of a promise would be as below,

    ```js
    const promise = new Promise(resolve => {
        setTimeout(() => {
            resolve("I'm a Promise!");
        }, 5000);
        }, reject => {

    });
    promise.then(value => console.log(value));
    ```