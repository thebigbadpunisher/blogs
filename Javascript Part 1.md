### Opening Google Chrome Console:
You can open Google Chrome console either by clicking three dots at the top right corner of the browser, selecting _More tools -> Developer tools_ or using a keyboard shortcut. 
**I prefer using shortcuts**: 
```javascript
Mac
Command+Option+J

Windows/Linux:
Ctl+Shift+J
```

We can write any JavaScript code on the Google console or any browser console. However, for this challenge, we only focus on Google Chrome console.

##### Console.log:
To write our first JavaScript code, we can use a built-in function **console.log()**. We passed an argument as input data, and the function displays the output. We passed `'Hello, World'` as input data or argument in the console.log() function.
```javascript
console.log('Hello, World!');
```

##### Console.log with Multiple Arguments:
The **`console.log()`** function can take multiple parameters separated by commas. The syntax looks like as follows: **`console.log(param1, param2, param3)`** 
```javascript
console.log('This', 'is', 'fun')
console.log('I', 'am', 'learning', 'Javascript', 'for', 'Hacking')
```

##### Comments:
We can add comments to our code. Comments are very important to make code more readable and to leave remarks in our code. JavaScript does not execute the comment part of our code. In JavaScript, any text line starting with // in JavaScript is a comment, and anything enclosed like this `//` is also a comment.

**Example: Single Line Comment**: 
```javascript
// This is the first comment  
// This is the second comment  
// I am a single line comment
```

**Example: Multiline Comment**: 
```javascript
/*
This is a multiline comment  
	Multiline comments can take multiple lines  
	 	JavaScript is the language of the web  
 */
```

##### Syntax:
The syntax is very informative. It informs what type of mistake was made. By reading the error feedback guideline, we can correct the syntax and fix the problem. The process of identifying and removing errors from a program is called **debugging**.

So far, we saw how to display text using the _`console.log()`_. If we are printing text or string using _`console.log()`_, the text has to be inside the 'ingle quotes, double quotes, or a backtick. **Example**: 
```javascript
console.log('Hello, World!')
console.log("Hello, World!")
console.log(`Hello, World!`)
```

#### Arithmetic:
In addition to the text, we can also do mathematical calculations using JavaScript. **Example**: 
```javascript
console.log(2 + 3) // Addition
console.log(3 - 2) // Subtraction
console.log(2 * 3) // Multiplication
console.log(3 / 2) // Division
console.log(3 % 2) // Modulus - finding remainder
console.log(3 ** 2) // Exponentiation 3 ** 2 == 3 * 3
```

---

### Adding JavaScript to a Web Page:
JavaScript can be added to a web page in three different ways:
- **_Inline script_**
- **_Internal script_**
- **_External script_**
- **_Multiple External scripts_**

The following sections show different ways of adding JavaScript code to your web page.
##### Inline Script: 
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>I love hacking Javascript !!!</title>
  </head>
  <body>
    <button onclick="alert(document.domain)">Click Me</button>
  </body>
</html>
```
We use inline script to add event handlers in html tags. We can create a pop up alert message using the _`alert()`_ built-in function with _`onclick`_ event handler which functions when the html tag is clicked.

##### Internal Script: 
The internal script can be written in the _`head`_ or the _`body`_, but it is preferred to put it on the body of the HTML document. First, let us write on the head part of the page.
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>I love hacking Javascript !!!</title>
    <script>
      console.log('HAHAHA!!!!!')
    </script>
  </head>
  <body></body>
</html>
```
This is how we write an internal script most of the time. Writing the JavaScript code in the body section is the most preferred option. Open the browser console to see the output from the `console.log()`.
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>I love hacking Javascript !!!</title>
  </head>
  <body>
    <button onclick="alert(document.domain);">Click Me</button>
    <script>
      console.log('HAHAHA!!!!!')
    </script>
  </body>
</html>
```

##### External Script: 
Similar to the internal script, the external script link can be on the header or body, but it is preferred to put it in the body. First, we should create an external JavaScript file with `.js` extension. All files ending with `.js` extension are JavaScript files.

External scripts in the _head_:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>I love hacking Javascript !!!</title>
    <script src="basic.js"></script>
  </head>
  <body></body>
</html>
```

External scripts in the _body_:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>I love hacking Javascript !!!</title>
  </head>
  <body>
    <!-- JavaScript external link could be in the header or in the body --> 
    <!-- Before the closing tag of the body is the recommended place to put the external JavaScript script -->
    <script src="basic.js"></script>
  </body>
</html>
```

**Multiple External Scripts**: 
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Multiple External Scripts</title>
  </head>
  <body>
    <script src="./helloworld.js"></script>
    <script src="./introduction.js"></script>
  </body>
</html>
```
_Your main.js file should be below all other scripts_. It is very important to remember this.

---

### Introduction to Data types:

In JavaScript and also other programming languages, there are different types of data types. The following are JavaScript primitive data types: _String, Number, Boolean, undefined, Null_, and _Symbol_.
##### Numbers:
- Integers: Integer (negative, zero and positive) numbers. **Example**: ... -3, -2, -1, 0, 1, 2, 3 ...
- Float-point numbers: Decimal number. **Example**: ... -3.5, -2.25, -1.0, 0.0, 1.1, 2.2, 3.5 ...

##### Strings: 
A collection of one or more characters between two single quotes, double quotes, or backticks. **Examples**: 
```javascript
'I'
'am'
'Nischal'
'Javascript sucks'
'But web hacking requires Javascript'
"Enough of using single quotes/apostrophies"
"Double quotes are love"
`But backticks are vulnerable to XSS`
`How? Because of template literals ${alert("HAHAHA")}`
`Enough!!!`
```

##### Booleans: 
A boolean value is either True or False. Any comparisons returns a boolean value, which is either true or false.
**Examples**: 
```javascript
true // if the light is on, the value is true
false // if the light is off, the value is false
```

##### Checking Data Types:
To check the data type of a certain variable, we use the **typeof** operator. **Examples**: 
```javascript
console.log(typeof 'Nischal') // string
console.log(typeof 5) // number
console.log(typeof true) // boolean
console.log(typeof null) // object type
console.log(typeof undefined) // undefined
```


---

### Variables:

Variables are _containers_ of data. Variables are used to _store_ data in a memory location. When a variable is declared, a memory location is reserved. When a variable is assigned to a value (data), the memory space will be filled with that data. To declare a variable, we use _var_, _let_, or _const_ keywords.

For a variable that changes at a different time, we use _let_. If the data does not change at all, we use _const_. For example, PI, country name, gravity do not change, and we can use _const_. We will not use var in this challenge and I don't recommend you to use it. It is error prone way of declaring variable it has lots of leak. We will talk more about var, let, and const in detail in other sections (scope). For now, the above explanation is enough.

A valid JavaScript variable name must follow the following rules:
- A JavaScript variable name should not begin with a number.
- A JavaScript variable name does not allow special characters except `dollar sign` and `underscore`.
- A JavaScript variable name follows a camelCase convention.
- A JavaScript variable name should not have space between words.

The following are examples of valid JavaScript variables.
```javascript
firstName
lastName
country
city
capitalCity
age
isMarried

first_name
last_name
is_married
capital_city

num1
num_1
_num_1
$num1
year2020
year_2020
```
The first and second variables on the list follows the camelCase convention of declaring in JavaScript. In this material, we will use camelCase variables (camelWithOneHump). We use CamelCase (CamelWithTwoHump) to declare classes, we will discuss about classes and objects in other section.

Let us declare variables with different data types. To declare a variable, we need to use _let_ or _const_ keyword before the variable name. Following the variable name, we write an equal sign (assignment operator), and a value(assigned data).
```javascript
// Syntax
let nameOfVariable = value
```

**Examples of declared variables**: 
```javascript
// Declaring different variables of different data types
let firstName = 'Nischal' // first name of a person
let lastName = 'Karki' // last name of a person
let country = 'Nepal' // country
let city = 'Bardibas' // capital city
let age = 23 // age in years
let isMarried = false

console.log(firstName, lastName, country, city, age, isMarried)
```

```javascript
// Declaring variables with number values
let age = 100 // age in years
const gravity = 9.81 // earth gravity  in m/s2
const boilingPoint = 100 // water boiling point, temperature in °C
const PI = 3.14 // geometrical constant
console.log(gravity, boilingPoint, PI)
```

```js
// Variables can also be declared in one line separated by comma, however It is recommended to use a seperate line to make code more readble
let name = 'Nischal', job = 'Hacker', live = 'Nepal'
console.log(name, job, live)
```
