# Max React Udemy
#react #javascript #udemy #course 

Gustav section recommendation: 1-10, 14, 16-18, 20-22, 24, 26

[Code](https://github.com/academind/react-complete-guide-code/tree/03-react-basics-working-with-components/code)
# Getting started
React is a JS library for building user interfaces

**JavaScript**
Run logic in the browser's loaded page
* Manipulate HTML structure (DOM) of the page

Con
* Imperative approach: with JS you need to write every single step that should be taken

**React**
* Declarative approach: makes creating modern, reactive user interfaces easier using a higher level syntax
* Split application into small building blocks/**compoents** where every component has a clear task
	* code stays maintainable and managable

## Install Node (Version 16)
```shell
nvm install 16.13.
nvm use 16.13.1
node --version
```

## Outline

![[Pasted image 20220706152253.png]]
# JavaScript refresher
Only making notes of things here that weren't covered in Mosh JS Beginner course.

## Exports & Imports
Need to export a variable/function/whatever in order to import it somewhere else.
```js script
// file: person.js
const person = {
	name: 'Gina'
}
export default person
```
```js script
// file: utility.js
export const clean = () => {...}
export const baseData = 10;
```

```js script
// file: app.js

// import default export from another file (doesn't matter what it is called)
import person from './person.js'
import prs from './person.js'

// import non-default export from another file (need to have same name as export)
import {baseData} from './utility.js'
import {clean} from './utility.js'

// import all
import * as bundeled from './utility.js'
```

## Classes
Can have inheritance
* `class Person extends Master`
	* `super` need to call in class that is inheriting
* There is also a more modern syntax
	* has the same advantage as all arrow functions have: The `this`  keyword doesn't change its reference.

```js script
// modern syntax
class Human {
	species = 'human';
}
 
class Person extends Human {
	name = 'Gina';
	printMyName = () => {
		console.log(this.name);
	}
}
 
const person = new Person();
person.printMyName();
console.log(person.species); // prints 'human'
```
```js script
// old approach
class Human {
	constructor() {
		this.gender = 'male';
	}
	printGender() {
		console.log(this.gender);
	}
}

class Person extends Human {
	constructor() {
		super(); // need to call in order to call Human constructor
		this.name = 'Gina';
		this.gender = 'female'; // can override inherited property
	}

	printMyName() {
		console.log(this.name);
	}
}

// instantiate class with new keyword
const myPerson = new Person();
myPerson.printMyName();
myPerson.printGender();
```

## Destructuring
Extract array elements or object properties and store them in variables

```js script
// assign a to Hello and b to World
[a, b] = ['Hello', 'World', 'Apple'];
console.log(a); // Hello
console.log(b); // World
[a, ,c] = ['Hello', 'World', 'Apple'];
console.log(a, c) // Hello Apple
```

## Array functions
Particularly important in this course are:

- [map()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map))
- [find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [findIndex()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex))
- [filter()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter))
- [reduce()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b))
- [concat()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b))
- [slice()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice))
- [splice()]([https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice))

# React basics & components
Declarative programming: We define the desired end-state and REact will then generate these instructions behind the scenes to bring that on your screen
## Component overview
**A Component is just a function**
* Can replace all function declarations
*  with arrow functions

* Components are reusable building blocks in your UI
	* combination of HTML, CSS, and JS

Component-Driven UIs allow for reusable code and separation of concerns
* Reusability: don't repeat yourself
* SoC: Don't do too many things in one and the same place

Good practice: 1 file per component

## Create new React App
Requirements: install Node.js version 16

`npx create-react-app` creates
* `package.json`
	* holds all the dependencies of this project
* `node_modules/`
	* Never edit this. It contains the downloaded modules based on the dependencies specified in `package.json`
* `src/`
	* This is where you're write your React code
	* What you need
		* `index.js`
			* first code file that will be executed when running `npm start`
		* `App.js`
			* imported into `index.js` 
		* `index.css`
			* imported into `index.js` to inject css into it
```shell
npx create-react-app react-app-name
cd react-app-name
npm start
```

## Download existing React App
If you download another react app, then you run `npm install` instead of `npm create-react-app` 
```shell
npm install
npm start
```

## Importing React
```js script
import ReactDOM from 'react-dom/client'
```

## Specify root html page
There is a file `public/index.html` which contains a `div` with the id `root` which the `index.js` file can replace with the content specified by the renderer by using the id.
* In this case we're replacing it with the App component
```html
<!--- index.html -->
<div id='root'></div>
```
```js script
// index.js
import ReactDOM from 'react-dom/client'
import './index.css';
import App from './App'; // App.js (when importing js you omit extension)

const root = ReactDOM.createRoot(document.getElementByID('root'));
root.render(<App />);
```

Render App component in the place of the content in `index.html` where the div id = root.
```js script
// App.js
function App() {
	return (
		<div>
			<h2>Let's get started!</h2>
		</div>
	);
}
export default App;
```

## JSX
JavaScript XML: write HTML in js file
* HTML == XML

May only have one root element per JSX snippet
* Solution: wrap all code in an outer `div`

```js script
  return (
    <div>
      <div>Date</div>
      <div>
        <h2>Title</h2>
        <div>Amount</div>
      </div>
    </div>
  );
```

## Building your first component
Seperate all components.

**A Component is just a function**

1. Create `src/components/`
	1. contains all components except `App.js` (our root component)
2. Create new js file
	1. convention: Pascal Case
3. Create JS function returning JSX
	1. convention: same as file name
4. Export component
5. Import component into App.js
6. Call component in the App's JSX
	1. `<ComponentName></ ComponentName>`

```js script
// components/ExpenseItem.js

function ExpenseItem() {
    return (
        <h2>Expense item!</h2>
    );
}

export default ExpenseItem;
```
```js script
// App.js

import ExpenseItem from "./components/ExpenseItem";

function App() {
  return (
    <div>
      <h2>Let's get started!</h2>
      <ExpenseItem></ExpenseItem>
    </div>
  );
}

export default App;
```

### Adding CSS
1. Add css file in `components/` with the same name as the component
2. import css into the component
3. In the `div` add `className="<cssClass>"`

```js script
// components/ExpenseItem.js

import './ExpenseItem.css';

function ExpenseItem() {
  return (
    <div className="expense-item">
      <div>7 July 2022</div>
      <div className="expense-item__description">
        <h2>Car Insurance</h2>
        <div className="expense-item__price">R1000.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

## Dynamic Data
Run/Inject JavaScript in HTML using `{}`
* Need to convert objects (such as Date objects) to display them in HTML

### Hardcoded data
```js script
import "./ExpenseItem.css";

function ExpenseItem() {
  const expenseDate = new Date(2022, 6, 22);

  return (
    <div className="expense-item">
	    {expenseDate.toISOString()}
    </div>
  );
}

export default ExpenseItem;
```

### Passing data with props
Pass data from component to component using props (properties/attributes).
* props = key, value pair

1. Create variables in the component where the data is coming from
2. `<ComponentName someAttribute={someAttributeValue}></ComponentName>`
3. In the target component, add a parameter
	1. convention: parameter = props 
		1. `function ComponentName2(props) {}`
4. Use the parameters in your component
	1. `props.someAttribute`
	2. someAttribute must be the same name for the attribute passed to the component
5. Format parameters to your needs
	1. Example format date object into human readable format

```js script
// App.js

import ExpenseItem from "./components/ExpenseItem";

function App() {
  const expenses = {
	  id: "e2",
	  title: "New TV",
	  amount: 799.49,
	  date: new Date(2021, 2, 12)
  };

  return (
    <div>
      <h2>Let's get started!</h2>
      <ExpenseItem title={expenses.title} amount={expenses.amount} date={expenses.date}></ExpenseItem>
    </div>
  );
}

export default App;
```

```js script
// components/ExpenseItem.js

import "./ExpenseItem.css";
import ExpenseDate from "./ExpenseDate";

function ExpenseItem(props) {
  return (
    <div className="expense-item">
      <ExpenseDate date={props.date}/>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">R{props.amount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

```js script
// components/ExpenseDate.js

function ExpenseDate(props) {
  const month = props.date.toLocaleString("en-UK", { month: "long" });
  const day = props.date.toLocaleString("en-UK", { day: "2-digit" });
  const year = props.date.getFullYear();

  return (
    <div>
      <div>{month}</div>
      <div>{year}</div>
      <div>{day}</div>
    </div>
  );
}
export default ExpenseDate;
```

## Wrapper components (composition)
Can wrap a component around another component (like a `div`)
* `props.children`
	* represents the content in between the component `<someComponent>This is content</>`

```js script
import Card from "./components/Card";

function App(){
  return (
    <Card>
      <h2>Let's get started!</h2>
      <Expenses expenses={expenses}/>
    </Card>
  );
}
```
```js script
import ExpenseItem from "./ExpenseItem";
import './Expenses.css'
import Card from './Card'

function Expenses(props) {
    let result = new Array();
    for (let expense of props.expenses) {
        result.push(<ExpenseItem title={expense.title} amount={expense.amount} date={expense.date}/>);
    }
  return <Card className='expenses'>{result}</Card>;
}
export default Expenses;
```

```js script
import './Card.css';

function Card(props) {
    const classes = 'card ' + props.className;
    return <div className={classes}>{props.children}</div>
}
export default Card;
```


# User Interaction & State
We want to react to user events and trigger a state change

## Event listening & handling
Pass **pointer** to function that needs to execute when an event occurs (not the full function)
* pass `eventHandler` not `eventHandler()`

Naming convention: end function name with `Handler`

### [Forms of user input](https://reactjs.org/docs/handling-events.html)
#### Buttons
```html
<button onClick={eventHandler}>Click me!</button>`
```
#### Forms
```html
<form onSubmit={eventHandler}>
	<button type='submit'>Submit</button>
</form>
```

## useState(): Updating what is on the screen
State allows for reactivity
* React does not call a compenent instance again after initial rendering, and hence we need to tell React that it should run a component again with state with `useState`

`useState` allows to define when it should reflect when a change to a value is made
* Need to set a default value
	* Only used if an instance's component has only been called once. Thus if we update the state it won't be overwritten with the default value when the component is called again (will only use the latest state of the variable)
* Returns the current state value and the updating function
	* Use updating function to change the value/state of the variable
		* When called, it causes React to call the component function again (with its new state and display any changes which it detects
* State updates a particular **instance** of a component's variables
* naming convention: `[var, setVar]`

`useState` Is a React hook
* Identified by the fact that it starts with `use`
* Must be called directly inside a React component function
	* not outside
	* not nested

```js script
// ExpenseItem.js

// change state
import { useState } from 'react';

import "./ExpenseItem.css";
import ExpenseDate from "./ExpenseDate";

function ExpenseItem(props) {
  // Returns the current value and the updating function
  const [title, setTitle] = useState(props.title);
  // update title
  const clickHandler = () => {
    setTitle("Updated!");
  };

  return (
    <div className="expense-item">
      <ExpenseDate date={props.date}/>
      <div className="expense-item__description">
        {/* use current state title */}
        <h2>{title}</h2>
        <div className="expense-item__price">R{props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change title</button>
    </div>
  );
}

export default ExpenseItem;
```

## User Form input
