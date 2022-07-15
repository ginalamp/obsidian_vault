# Master the Fundamentals in 6 hours
#javascript #course #udemy

[JavaScript - Master the Fundamentals in 6 Hours (Mosh)](https://shoprite.udemy.com/course/javascript-basics-for-beginners/learn/lecture/10688604)

* Source code: [here](https://shoprite.udemy.com/course/javascript-basics-for-beginners/learn/lecture/10689626#notes)

# Getting Started

## Overview

**Functions**
* Web / Mobile apps
* Command line tools
* Games

**Browser JavaScript Engine**
* Firefox: SpiderMonkey
* Chrome: v8

**Run JS Outside browser: Node**
	* Node: C++ program that include's Google's V8 JavaScript engine
	* Pass JS code to Node for execution

**Seperation of concerns**
* Put js code in seperate file

**In line JS (don't do this - rather seperate concerns)**
* Put scripts at end of body: html files get executed from top to bottom
* script placement best practice: put at end of body (such that the browser doesn't execute the script as things are loading)

## Dev Setup

Download [node.js](https://nodejs.org/en/)

VS Code
* Shortcut: `! + <tab>` generates boilerplate html code
* Extension: live server
	* Open html with live server extension (right click > open with live server)


## JS in browsers
Log something to console
* Shortcut: `option + command` view console in browser
```js script
<script>
	console.log("heyo");
</script>
```


## JS in node
Run JS code in terminal using node.js
```shell
node <file>.js
```

# Basics
## Variables
Assign variables with `let`
```js script
let name = "Gina";
console.log(name);
```

Conventions
* camel case
* cannot start with number
* cannot contain space or hypen
* case sensitive
* declare multiple variables each on a new line

## Constants
Assign variables with `const`
```js script
const interestRate = 0.3;
console.log(interestRate);
```

## Primitive types
* String
* Number
* Boolean (`true`, `false`)
* undefined (default value for variable or explicitly set to `undefined`)
* null (`null`)


## Dynamic types
* variable type can change

## Reference types
Objects, arrays, functions

### Object
* Denoted with `{}`
* Key-value pairs in object
```js script
// set object
let person = {
	name: "Gina",
	age: 22
};
console.log(person);

// change object property
person.name = 'Heinrich';
person['name'] = 'Heinrich';
console.log(person.name);
```

### Array
* Denoted with `[]`
* Index from 0
* An array is an object in js
```js script
// set array
let colors = ['red', 'blue', 'yellow']
console.log(colors);

// set & access array properties
console.log(colors[0]);
colors[3] = 'purple';
console.log(colors.length)
```


### Function
Set of statements that performs a task or returns a value
```js script
function funcName(name) {
	console.log("Hi " + name);
}
funcName('Gina');
```


# Operators
* Arithmetic
* Assignment
* Comparison
* Ternary
* Logical
* Bitwise

## Arithmetic
* `+, -, *, /, %, ** `
* Increment: ++
```js script
let x = 6;
// increment before display
console.log(++x);
// increment after display
console.log(x++);
```
* Decrement: --
	* same logic as increment

## Assignment
```js script
let x = 10;
x = x + 5;
x += 5; // shorthand
```

## Comparison
* relational operators: `>, <, >=, <=`
* strict equality: `===`, `!==`
	* same type + value
* loose equality: `==`, `!=`
	* same value (but not necessarily same type)

## Ternary
Shorthand if statement
* `boolean ? <valueIfTrue> : <valueIfFalse>`

```js script
let points = 110;
let type = points > 100 ? 'gold' : 'silver';
console.log(type)
```

## Logical
* && -> and
* || -> or
* ! -> not

```js script
// booleans
console.log(true && true);
console.log(true || false);
console.log(!true);
```

### Truthy & Falsy
* Falsy
	- undefined, null, 0, false, '' , NaN
- Truthy
	- anything that is not falsy
	- short circuiting: return first truthy value (order specified)

```js script
// non-booleans
console.log(false || "Gina"); // returns 'Gina'
console.log(false || 66); // returns 66
console.log(false || 66 || "Gina"); // returns 66 (first truthy value)
```

## Bitwise
* or: |
* and: &

## Operator precedence 
* BOTMAS


# Control Flow

## If... else
* single line: no brackets required
* multi-line: `{}` brackets required
```js script
if (condition) {
	statement
}
else if (anotherCondition) {
	statement
}
else {
	statement
}
```

## Switch... case
```js script
let role;

switch (role) {
	case 'guest':
		console.log('Guest User');
		break; // required - otherwise all case statements after this will execute
	case 'moderator':
		console.log('Moderator User');
		break;
	default:
		console.log('Unknown User');
}
```

## Loops
### For loop
```js script
for (let i = 0; i < 5; i++) {
	statement
}
```

### While loop
```js script
let i = 0;
while (i < 5) {
	statement
	i++;
}
```

### Do while loop
* Always executed at least once (even if the condition is false)
```js script
let j = 0;
do {
	statement
	j++;
} while (j < 5);
```

### For in loop
```js script
const person = {
	name: 'Gina',
	age: 22
};

for (let key in person) {
	console.log(key, person[key]);
}

const colors = ['red', 'green', 'blue']
for (let index in colors) {
	console.log(index, colors[index]);

}
```

### For of loop
Like python for in loop
```js script
const colors = ['red', 'green', 'blue']
for (let color of colors) {
	console.log(color);
}
```


### Break & Continue
* Break: b
* reak out of loop
* Continue: jump to beginning of loop & execute next iteration

# Objects
## Basics
Create object using object literal syntax with a function.
```js script
const circle = {
	radius: 1,
	location: {
		x: 1,
		y: 2
	},
	isVisible: true,
	// can have method as part of object
	draw: function() {
		console.log('draw');
	}
};

// call draw method of circle object
circle.draw();
```

## Factory function
* camel notation
```js script
// factory function
function createCircle(radius, location) {
    return {
        radius: radius, // can shorten by just saying radius (since same name)
        location,
        // can remove function() keyword when method (ie part of object) 
        draw() { 
            console.log('draw');
        }
    };
}
console.log(createCircle(1, {x:1, y:2}));
console.log(createCircle(2, {x:5, y:9}));

// another example
function createAddress(street, city, zipCode) {
    return {
        street,
        city,
        zipCode
    };
}
console.log(createAddress('21 Blue Street', 'Amsterdam', 8001));
```

## Constructor function
* pascal notation (camel case with first letter also being caps)
* `this` references the object that is executing the constructor function
* `new` 
	1. creates an empty js object
	2. points `this` to the new object
	3. returns created `this` object

```js script
function Circle(radius) {
    this.radius = radius;
    this.draw = function() {
        console.log('draw');
    }
}
console.log(new Circle(55));

// another example
function CreateAddress(street, city, zipCode) {
    this.street = street;
    this.city = city;
    this.zipCode = zipCode;
}
console.log(new CreateAddress('21 Blue Street', 'Amsterdam', 8001))
```

## Object properties are mutable
Even though an object might have be a `const`, the properties within the object are mutable. The `const` keyword just means that the variable name may not be set to something that it wasn't originally set to.

```js script
const circle2 = {
    radius: 1
};
// set object properties
circle2.color = 'yellow';
circle2.draw = function() {}
console.log(circle2)
delete circle2.color;
delete circle2.draw;
console.log(circle2)

// cannot reset variable
circle2 = {}; // illegal: immutable
```

## Constructor
Every object has a constructor (a function that was used to create that object)

```js script
new String(); // '', "", ``
new Boolean(); // true, false
new Number(); // 1, 2, 3, ...
```

## Functions are objects
```js script
<function>.name // number of args
<function>.call({}, arg) // synonymous with new
<function>.apply({}, listOfArgs)
```

## Primitives vs Reference types
* Primitives are independent of one another
	* a change in `x` (if `y = x`) will not change `y`
* References are dependent on one another
	* a change in `person1.value` (if `person2 = person1`) will change `person2.value`

```js script
// variable copies
let x = 10;
y = x;
x += 1;
console.log(x, y); // x=11, y=10

const x = {value: 10};
y = x;
x.value += 1;
console.log(x, y); // x=11, y=11

// functions
let number = 10;
function changeX(number) {
	number += 1;
}
changeX(number);
console.log(number); // number=10

let obj = {value: 10};
function changeX(obj) {
	obj.value += 1;
}
changeX(obj);
console.log(obj); // obj=11

```

## Enumerating object properties
* note: `Object.entries` doesn't work with node for some reason
```js script
// key-value indexing
for (let key in circle)
	console.log(key, circle[key]);

// keys
for (let key of Object.keys(circle))
	console.log(key);
// values
for (let entry of Object.entries(circle))
	console.log(entry);
```

## Object cloning
Copy object properties to new object
```js script
// spread object: copies circle properties to between the {}
const another = { ...circle};

// assign: add circle properties to {} object
const another2 = Object.assign({}, circle);

// assign: add circle properties to {color: 'yellow object'}
// another3 has all circle properties and color property
const another3 = Object.assign({color: 'yellow'}, circle);
```

## Garbage collection
* javascript automatically deallocates unused variables

## Built-in Objects
### Math
**Some useful methods**
* `Math.random()`
	* Random number between 2 numbers
* `Math.round()`
* `Math.max()`, `Math.min()`
	* Min/max number in list

### String
String primitive & string object
* javascript automatically wraps string primitives as string objects, so we can call methods on strings
```js script
// string primitive
const m1 = 'This is my first message';
// String object
const m2 = new String('hi');
```
**Some useful methods**
* `m1.length`
	* number of characters in string
* `m1[index]`
	* index into string characters
* `m1.includes(substring)`
	* check if string contains a certain substring
* `m1.startsWith(substring)`, `m1.endsWith(substring)`
	* check if string starts/ends with a certain substring
* `m1.indexOf(substring)`
	* check at which index of the string a certain substring starts at
* `m1.replace(substring, replaceVal)`
	* replace substring with another value
* `m1.toUpperCase()`, `m1.toLowerCase()`
	* convert string to upper/lower case
* `m1.trim()`, `m1.trimLeft()`, `m1.trimRight()`
	* Remove all whitespace before & after string
* `m1.split(char)`
	* split string into array based on a given character

### Date
Constructors
```js script
const now = new Date(); // current date/time
const date1 = new Date('Jan 11 2018 09:00'); // look at dateString to see supported formats
const date2 = new Date(2018, 0, 11, 9, 0) // date object
```

**Some useful methods**
* get...
* set...
* `toDateString()`
	* date component of datetime obj
* `toTimeString()`
	* time component of datetime obj
* `toISOString()`
	* common format to transfer date between client and server

## Template literals
Format string the way you want the output to look like by encasing it in \`\`
```js script
let name = 'John'; // use ${name} to referance var in string

// will output according to formatting in ``
const message = 
`Hi ${name},

Thank you for joining my mailing list. You're number ${4 + 5} on the list!

Regards,
Gina`;
```

## Object equality
Solve any issues with lodash installation [here](obsidian://open?vault=Obsidian%20Vault&file=JavaScript%2FErrors%20or%20Mac%20Issues)
```js script
import _ from 'lodash'; // check object equality

const address1 = new CreateAddress('a', 'b', 'c');
const address2 = new CreateAddress('a', 'b', 'c');

console.log(_.isEqual(address1, address2)); // true
```

# Arrays
* `const` does not stop us from modifying the array

## Adding elements
* `push()`
* `unshift()`
* `splice()`
```js script
const numbers = [3,4];

// add to end
console.log(numbers.push(5, 6));

// add to beginning
console.log(numbers.unshift(1,2));

// add to specific position splice(startIndex, deleteNumber, elementsToAdd...)
console.log(numbers.splice(2, 0, 'a', 'b'));
```

## Finding elements
* `indexOf()`
	* returns -1 if doesn't exist
	* can also pass additional argument to state at which index it should start searching from
```js script
const numbers = [1, 2, 3, 1, 4];

// get index of first occurance of given item
console.log(numbers.indexOf(1))
// get index of last occurance of given item
console.log(numbers.indexOf(1))

// check if given element exists in arr
console.log(numbers.includes(1))
```

### Reference types
* `find()`
	* returns `undefined` if element not found
	* pass function to `find()` method which is then applied to each element in the array until the **first** instance where the function returns `true` is found. The element that satisfies the `true` condition is then returned

```js script
// find element in reference type
const obj = [
    {id: 1, name: 'a'},
    {id: 2, name: 'b'}
]
console.log(obj.find(function(element) {return element.id == 2}));
console.log(obj.findIndex(function(element) {return element.id === 2}));
```

## Arrow functions
1. remove `funcion keyword`
2. add `=>` between param and `{}`
3. Params
	1. 1 param: remove `()`
	2. 0 param: `() => {...}`
4. Single line of code
	1. remove `return` and `{}`
	2. put everything on one line

```js script
// og function
console.log(obj.find(function(element) {return element.id === 2}));

// arrow function
console.log(obj.find(element => element.id === 2));
```

## Remove elements
* `pop()`
* `shift()`
* `splice()`

```js script
const numbers = [1, 2, 3,4];

// remove last element & return it
console.log(numbers.pop());

// remove first element & return it
console.log(numbers.shift());

// add to specific position splice(startIndex, deleteNumber)
console.log(numbers.splice(2, 1));
```

## Emptying an Array
Remove all elements from an array
* Once an array is empty and not used the garbage collector will automatically deallocate its memory
```js script
arr.length = 0;
```

## Combining & Slicing arrays
**Primitive types:** copied by value; **Reference types:** copied by reference
* `concat()`
* `slice()`
	* \[start, stop)
	* Exclude stop to get all elements from start to end of array
	* Exclude both params to copy array
```js script
const first = [1,2,3];
const second = [4,5,6];

// combine arrays
const combined = first.concat(second);

// slicing [start, stop)
combined.slice(2, 4);

// copy array
combined.slice;
```

### Spread operator
Take all elements from array and copy it over.
```js script
console.log(...first, 'a', ...second, 'b');
```

## Iterating an Array
* `forEach(function)`
	* executes function for each element of the array

```js script
numbers.forEach(number => console.log(number));
numbers.forEach((number, index) => console.log(index, number));
```

## Array <-> String
* `join()`
	* array -> string with string containing the specified seperator (or `,` as default)
* `split()`
	* string -> array based on specified seperator
		* If omitted, a single-element array containing the entire string is returned.
```js script
// array to string
const joined = numbers.join();
console.log(joined);

// string to array
console.log(joined.split(','));
```

**Commonly used to create url slug**

```js script
const message = "This is a string";

// converts "This is a string" to "This-is-a-string"
console.log(message.split(' ').join('-'));
```


## Sorting Arrays
* `sort()`
	* converts each element to a string and then sort in ascending order
	* object sort: create comparative function
		* sort objects by specifying function to compare objects with
		* default sort by first key's value
* `reverse()`
	* sort, but descending order

```js script
// sort array
const nums = [5,2,3,4];
console.log(nums.sort());
console.log(nums.reverse());

// sort object by creating a comparitive function
const courses = [
	{id: 1, name: "Node.js"},
	{id: 2, name: "JavaScript"}
]
console.log(courses.sort(function(obj1, obj2) {
    // convert to upper (ascii representation sees upper > lower)
    const name1 = obj1.name.toUpperCase();
    const name2 = obj2.name.toUpperCase();

    if (name1 > name2) return 1;
    if (name1 < name2) return -1;
    return 0;
```

## Test all elements in array
* `every()`
	* test whether every element in the array meets a certain condition
	* runs until `false` condition is met (if not met then it returns `true`)
* `some()`
	* test whether there exists an element in the array that meets a certain condition
	* runs until `true` condition is met (if not met then it returns `false`)

```js script
const numbers = [1,2,3];

// check if all numbers in the array are positive
console.log(numbers.every(element => element > 0));

// check if there exists a positive number in the array
console.log(numbers.some(element => element > 0));
```

## Filtering an array
Filter array based on search criteria
* `filter(function)`
	* apply function to every element in the array and return a new array with elements satisfying the function's condition

```js script
const numbers = [1,-1,2,3];

// get positive numbers in array
console.log(numbers.filter(element => element >= 0));
```

## Mapping an array
Map each item in an array to something else
* `map(function)`
	* apply function to every element in the array and return a new array in the format specified in the function

```js script
const filtered = [1,-1,2,3].filter(n => n >= 0);

// map positive numbers to html bullet syntax
const items = filtered.map(n => '<li>' + n + '</li>');
// convert array of strings to string
const html = '<ul>' + items.join('') + '</ul>';
console.log(html);

// map positive numbers to object property
console.log(filtered.map(n => ({value: n})));
```

## Reducing an array
Reduce all the elements in an array to a single value

* `reduce(function(accumulator, currentValue))`
	* `accumulator` stores the result of the function applied to the previous elements in the array
		* set to the first element if not initialised, and then the function starts from the second element onward
	* `currentValue` current element in the array (the reduce function gets applied to every element in the array)

```js script
// without initialisation
console.log(numbers.reduce((accumulator, currentValue) => accumulator + currentValue));

// with initialisation (init to 0)
console.log(numbers.reduce((accumulator, currentValue) => {
	return (accumulator + currentValue)}, 0));
```

## Check if something is an array
`Array.isArray(arr)`

# Functions
## Hoisting
JavaScript engine moves all function declarations to the top of the file, allowing one to be able to call a function before it is declared.

## Varied number of arguments
* `arguments` is associated with a function, where it contains all the values sent to the function (among other properties)
```js script
function sum() {
	let total = 0;
	for (let value of arguments)
		total += value;
	return total;
}
console.log(sum(1,2,3,4,5,10));
```

## Rest operator
* `...` Converts arguments sent to a function to an array
	* Gets the rest of the arguments that don't have an explicit parameter allocated to them

```js script
// sum all
function sum(...args) {
	return args.reduce((sum, curr) => sum + curr);
}
console.log(sum(1,2,3,4,5,10));

// apply 10% discount to sum
function sumWithDiscount(discount, ...args) {
	const total = args.reduce((sum, curr) => sum + curr);
	return total * (1-discount);
}
console.log(sumWithDiscount(0.1, 1,2,3,4,5,10));
```

## Default parameters
`function(param1, param2=defaultVal)`

## Getters & Setters
* `get` add keyword before function name in an object to make the function a getter
* `set` add keyword before function name in an object to make the function a setter
```js script
const person = {
	firstName: 'Gina',
	lastName: 'Lamprecht',
	// getter
	get fullName() {
		return `${person.firstName} ${person.lastName}`
	},
	// setter
	set fullName(value) {
		const parts = value.split(' ');
		this.firstName = value[0];
		this.lastName = value[1];
	}
}
// get full Name
console.log(person.fullName);

// set full name
person.fullName = 'John Smith';
console.log(person.fullName);
```

## Try and catch
Defensive programming: do error handling at the beginning of a function

* `throw new Error('messageToDisplay')`
	* throw exception
* `try` try executing a statement
* `catch(e)` if the statement results in an exception being thrown, this will cath that error
	* `alert(e)` displays error to user (note - this is an old way to do this)

```js script
const person2 = {
	firstName: 'Gina',
	lastName: 'Lamprecht',
	set fullName(value) {
        // handling errors
        if (typeof value !== 'string')
            throw new Error("Name must be string.");
        if (value.length !== 2)
            throw new Error("Enter first & last name.");

		const parts = value.split(' ');
		this.firstName = parts[0];
		this.lastName = parts[1];
	}
}
try {
    person2.fullName = null;
}
catch (e) {
    alert(e); // this is a bad way to do this!
}
```

## This keyword
`this` refers to the object that is executing the current function

* method (function part of object)
	* `this` references that object itself
* function
	* `this` refers to the global window object
		* note that when you have a method that calls a `function`, the `this` in that function also references the global window object. To change this, you should use an arrow function instead of a declared function with the function keyword.
* constructor function
	* `this` references a new empty object
	* called by the new operator, which calls a new empty object and causes `this` to point to the empty object

### Changing this
* Use arrow function instead of function keyword when you have a function within an object

```js script
const video = {
	title: 'a',
	tags: ['a', 'b', 'c'],
	showTags() {
		this.tags.forEach(tag => {
			console.log(this.title, tag);
		})
	}
}
```

## Sum of items
```js script
// exercise: sum of variable number of args
function sum3(...items) { // rest args into array
    if (items.length === 1 && Array.isArray(items[0]))
        items = [...items[0]]; // spread array to string
    return items.reduce((sum, curr) => sum + curr);
}
console.log(sum3(1,2,3,4));
console.log(sum3([1,2,3,4]));
```