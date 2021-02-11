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

3. What is Classes Hoisting?

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