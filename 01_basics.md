<a name="basics.md"></a>
# **Module #1 - The Basics**
---

<a name="loading"></a>
## **LOADING AND RUNNING JAVASCRIPT**

add `<script>` tag just before the `</body>` tag.

```html
<body>
  ...
  <script src="./some.js"></script>
</body>
```

<br>

<a name="variables"></a>
## **VARIABLES**

- **var** (_value can be updated_)
- **let** (_value can be updated_)
- **const** (_value can't be updated_)

```js
var name = "Wes";
let age = 100;
const cool = true;
```

<a name="typpeOfVariables"></a>
## **TYPE OF VARIABLES:**

<a name="strings"></a>
- ### String: 
  represent letter, pharagraphs, phases, etc. Can be declared with quotes, double-quotes or back ticks.

  ```js
  const name = "Wes";
  const middle = "topher";
  const last = `Bos`;
  ```

  sentence  
  with "\ esc", quotes, single quotes and backtip option:  
  sentence = She´s so "cool"

  ```js
  const sentence = 'she´s so "cool"';
  const sentence = "she´s so \"cool\"";
  const sentence = `She's so "cool"`;
  ```
  contatenation & interpolation  
  ```js
  const hello = `hello my name is ${variable_name} nice yo meet you. I'm ${30 + 5} years old` 
  ```

<a name="numbers"></a>
- ### Numbers:  
  Numbers on Javascript includes float, integers, etc ...  
  there are all the basic operation (addition, substraction, multiplication and division).

  ```js
  let a = 10 + 10 // addition
  let b = 20 - 10 // subtraction
  let c = 10 * 10 // multiplication
  let d = 100 / 10 // division
  let e = 1000 % 3 // modulo
  ```
  Javascript have helper methods like:  
  
  ```js
  Math.round(20.5) //result 21, round number up or down
  Math.floor(20.2) //result 20, will give you the lower
  Math.ciel(20.9) // result 21, will give you the upper
  Math.random() // gives random number between 0 and 1
  ```

  NaN is an other number, that means _Not a number_
  
  ```js
  let a = 10 / 'dog';
  console.log(a)

  // result: NaN
  ```

<a name="objects"></a> 
- ### Objects 
  Everything in javascript is an object, are use for collections of data or functionality.

  ```js
  const person {
    firstName = 'Cesar',
    lastName = 'Gomez',
    age = '35'
  };
  ```
  order doesn't matter in objects, we can access to the properties, the easiest way is:

  ```js
  person.firstName // access to the first name properti
  person.lastName // access to the last name properti
  person.age // access to the age properti
  ```

<a name="null_undefined"></a> 
- ### Null and Undefined  
  **Undefined:** comes when you try to access toa variable that has been created, but not set.

  ```js
  let dog;
  console.log(dog);  //result should be undefined
  ```

  **Null:** is a value of nothing  

  ```js
  let somethingNull = null; 
  ```
<a name="booleans"></a> 
- ### Boolians and equiality  

  **Booleans:**  is a value of true or false, can be manually set or calculate:

  ```js
  //manually set
  let isDrawing = true;

  //calculate
  const age = 18;
  const ofAge = age > 19;
  console.log(ofAge); // result should be false
  ```

  **Equality:** we have:  
  - = (setting or updating a variable)
  - == (it compares the value but not the type of )
  - === (compares the value and type of )

  ```js
  // =
  let dog = 'Sharon';

  // ==
  "10" == 10 //result is true, it compares the value but not the type of (both values are 10)

  // ===
  "10" === 10 // result is false, compares value and type of (first one is string, second one is number)
  ```  

<br>

---
back to [Table of Content](tableOfContent.md)  
next [Functions](02_functions.md)  