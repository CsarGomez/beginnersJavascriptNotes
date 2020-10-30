<a name="bits"></a>  
## **The tricky bits**
---

<a name="scope"></a> 
- ## Scope  
  <a name="globalVariables"></a>
  - ### Global variables  
    when variable is created a variable not inside a function,  not inside a module, not inside if statement, you can access   them from any other javascript that's running on the page   via script tag or console.
    in the brownser the global scope is called **_window_**

    ```js
    windows.setTimeOut();
    ```
    Var variables are attached to the window object and they are  globaly scoped, const and let still beign global scope but   not attached to the window.
    functions are attached to global scope as well

  <a name="functionScope"></a>
   - ### function scope
      when variables are created inside a function, those  variables are only a available inside of that function   unless we were to exolicitly return it and put it into it's   own variable when that function is run

      ```js
      const age = 100;

      function go(){
        const hair = 'blonde';
      }
      go();
      console log (hair); // this gives you an error because hair variable is inside of a function
      console.log(age);

      // right way to do it:
      const age = 100;

      function go(){
        const hair = 'blonde';
        console log (hair);
      }
      go();
      console.log(age);

      // also you can access to global variables from inside of a function
      const age = 100;

      function go(){
        const hair = 'blonde';
        console log (hair);
        console.log(age);
      }
      go();
      ```
  <a name="blockScope"></a>
  - ### block scope 
    var let and const variables are scoped differently  

    ```js
    if (1===1){
      let cool = true;
    }
    console.log(cool)
    ```  
    when you have a set of curly brackets "{...}" that is what is referred to as a block.
    you will not be able to access to the cool variable, because is inside of curly brackets.
    the solution will be to create a variable above it and updated inside the block.  
  
    ```js
    let cool;

    if (1===1){
      cool = true;
    }
    console.log(cool)
    ```  
    or

    ```js
    function isCool(name){
      let cool;
      if (name === 'wes'){
        cool = true;
      }
      return cool;
    }
    ```
<a name="hoisting"></a> 
- ## Hoisting
  Hoisting allows you to access functions and variables before they have been created, there´s two things in javascript that are hoited:
    - functions declarations

        ```js
          sayHi();

          function sayHi(){
            console.log('Hey!');
            console.log(add(10, 2));
          }

          function add(a, b){
            return a + b;
          }
        ```
    - variable declarations  
        javascript hoist variable declarations, but will not hoist the actual setting value:

        ```js
        // this will give you undefined
        console.log(age);
        var age = 10;

        //Reference error if you use let (age is not defined)
        console.log(age);
        let age = 10;
        ```

<a name="closures"></a> 
  - ## Closures 
    Closures are the ability for a child function or inner function (child scope) to access variables from a higher level scope (parent scope) even after the functions have been called or closed  

    ```js
      function parentScope(){
        const partetVar = 'I am the parent variable';
        function childScope(){
          const childVar = 'I am the child variable';
          console.log(childVar);
          console.log(paretVar)
        }
        return childScope;
      }

      const childFinal = parentScope();
      childFinal();
    ```

    in the example below, you stick a function into a variable and at a later point you have access to that child function.
    the closure is the fact that even though the parent function is done still maintain the variable in memory and you are able to access at later time.  
