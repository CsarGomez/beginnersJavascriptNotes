
<a name="functions"></a>  
# **Functions**
---

<a name="buildFunctions"></a>
## **Build functions**
  Functions can do anything, they´re group togeher set of instructions, often taking in values, doing some work and then returning a new value or set of values.  

  Functions are create or defined and then they later can be call.

  the function calculate bill will calculate what the bill would be regarding how much the tip was and how much the tax is.


  ```js
  // create or defined a function
  function calculateBill() {
    const total = 100 * 1.13;
    return total;
  }

  // call a function
  calculateBill();
  ```

  the total is not available out of the function, because we need to capture the return value of the function into a variable:

  ```js
  const myTotal = calculateBill();
  ```

<a name="parametersArguments"></a>
## **Parameters and arguments**
  ![parameters and arguments](function-definition.jpg)
  
  function using parameters and arguments

  ```js
  function calculateBill(billAmount, taxRate){
    const total = billAmount * (1 + taxRate);
    return total
  }

  const myTotal = calculateBill(500, 0.3);
  ```
  you can pass expresions to a function

  ```js
  const myTotal = calculateBill(20 + 20 + 30 + 20, 0.3);
  ```

  and also you can pass functions as arguments

  ```js
  function doctorize(firstName){
    return `Dr. ${name}`;
  }  

  function yell(name){
    return `Hey ${name.toUpperCase()}`;
  }

  yell(doctorize('Cesar'));
  // return "Hey DR. CESAR"
  ```

  you can set default values to the parameters: 

  >taxRate = 0.13  
  >tipRate = 0.15  

  if no one pass the parameter taxRate and tipRate for calculateBill function it will take by default the 0.13 for tax rate and 0.15 for tip rate

  ```js
  function calculateBill(billAmount, taxRate = 0.13, tipRate = 0.15){
    const total = billAmount + billAmount * taxRate + billamount * tipRate;
    return total
  }

  calculateBill(100);
  ```

  if you want to use only one of the defaul values, like tipRate but not taxRate
  ```js
  calculateBill(100, undefined, 0.2);
  ```
  the undefined will fallback to the defaul value of 0.13 for taxRate

<a name="waysFunctions"></a>
## **Different ways to declare functions**
  
  Javascript functions are values in themself that can be stored into variables or can be passed into other fucntions.

  there are different ways to declare functions

  <a name="regular"></a> 
  - ### Regular funcion declaration

    ```js
    function doctorize(firstName){
      return `Dr. ${fistName};
    }
    ```

  <a name="anon"></a>   
  - ### Anonymous function 
    is a fucntion without name 

    ```js
    function (firstName){
      return `Dr. ${fistName};
    }
    ``` 

  <a name="expression"></a>   
  - ### Function Expression 
    is an anonymous function stored into a variable 

    ```js
    const doctorize = function (firstName){
      return `Dr. ${fistName};
    }
    ```    
    the difference between regular function declaration and function expression is how they operate on the hoisting

  <a name="arrow"></a>  
  - ### Arrow Function  
    are anon functions, always need to be sticky into a variable.

    ```js
    //regular fucntion:
    function inchToCM(inches){
      const cm = inches * 2.54;
      return cm;
    }

    //arrow function:
    const inchesToCm = inches => inches * 2.54;
    ```

    other example:

    ```js
    //regular fucntion:
    function add(a, b=3){
      const total = a + b;
      return total;
    }

    //arrow fucntion
    const add = (a, b=3) => a + b;
    ```

    you cannot delete the _()_ on _(a, b=3)_ becuase there are  more than one parameter.  

  <a name="returnObject"></a>
  - ### Returning an Object

    ```js
    //regular fucntion:
    function makeABaby(fisrName, lastName){
      const baby = {
        name: `${first} ${last}`,
        age: 0
      }
      return baby;
    }

    //arrow fucntion:
    const makeABaby = (first, last) => {
      return baby = {
        name: `${first} ${last}`,
        age: 0
      }
    }

    //arrow fucntion 2:
    const makeABaby = (first, last) => ({ name: `${first} ${last}`, age: 0 });
    ```

  <a name="iife"></a>
  - ### IIFE  
    means Immediately Invoked Function Expression  

      ```js
      //anon function
      function(){
        console.log('Running the anon funciton');
        return 'you are cool';
      }

      //you can run immediately by doing this:
      (function(age){
        console.log('Running the anon funciton');
        return `you are cool and age ${age}`;
      })(10);
      ```

  <a name="mothods"></a>
  - ### Methods  
      is a function that lives inside an object like:

      ```js
      console.log
      ```  

      Log is the function that lives inside the console which is the Object  
      we can create our own methods:

      ```js
      const wes = {
        name: 'wes bos',
        sayHi: function(){
          return `Hey! wes`;
        },
      }
      ```

      there is a shorthand for that

      ```js
      const wes = {
        name: 'wes bos',
        sayHi(){
          return `Hey! wes`;
        },
      }
      ```

      and we can setup as an arrow function but you cannot access to the .this.

      ```js
      sayHi() => `Hey! wes`;
      ```

  <a name="callback"></a>
  ## **Callback functions**

  - **click callback function**

      ```js
      const button = document.querySelector('.clickMe');

      function handleClick(){
        console.log(great click);
      }

      button.addEventListener('click', handleClick);
      ```
      is a function passed into other funcion, that then can  be   called by the browser at a later point.

  - **timer callback function**

      ```js
      setTimeout(function()){
        console.log('Time to eat!');
      }, 1000);
      ```
      this will run after 1000 ms 

<br>

---
back to [Table of Content](tableOfContent.md)  
previous [The basics](01_basics.md)  
next [The Tricky Bits](03_bits.md)