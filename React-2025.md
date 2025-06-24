<https://www.udemy.com/course/react-the-complete-guide-incl-redux>

Started course on Wednesday, March 27, 2025.

To access a browser-based development environment, go to <https://react.new>

## Section 2: JavaScript Refresher

### Adding JavaScript to a Website

CodeSandbox link: <https://codesandbox.io/p/sandbox/javascript-refresher-start-rytt3j?file=%2Findex.html>

GitHub Repository with course notes and resources: https://github.com/academind/react-complete-guide-course-resources 

There are two main methods for adding JavaScript to a website:

*   Between `<script>` tags:

    ```html
    <script>
     alert('Hello'); 
    </script> 
    ```

*   Via `<script>` import

    ```html
    <script src="script.js"></script>
    ```

Adding the `defer` argument to a `script` element ensures that the rest of the page's HTML renders before the script is imported and the code is executed.

Adding `type="module"` to a `script` element unlocks certain syntax within the JavaScript file, including the ability to use `import` and `export` tags to access code in other files.

### Import and Export

The `export` keyword allows a variable, class, function, etc from one file to be used in another file. The referencing file must `import` the code to access it.

```javascript
export let apiKey = "adsgojjgsgosf"; 
// 
import { apiKey } from './util.js'
```

When referencing another file, use:

*   `./` to reference the current folder

*   `../` to reference the folder 1 level up

Including the file extension on an import is important, but the React build process often makes it unnecessary.

Using the `default` keyword in an `export` statement changes the syntax.

```javascript
export default "adsgojjgsgosf";
//
import apiKey from './util.js'; 
```

Note that the curly braces aren't used in this example. When importing from a file with a default export defined, you can set whatever variable name you want for it (so `apiKey` could be anything in this example). However, if a default is *not* defined, the curly braces **and** the same variable name from the exporting file must be used.

A file can export multiple things, but it can only have one default export.

If a file has multiple named exports, they can be imported in multiple ways:

```javascript
export default "abc"; 
export let y = 123; 
export let z = "eat it"; 
//
import { y, z } from './util.js'; 
// OR
import * as util from './util.js'; 
```

The second option imports all the exported items as a single JavaScript object. The default export is available in that JavaScript object via `util.default`.
The `as` keyword can also be used to rename an imported thing. E.g. `import {x, y as z} from './util.js';`

### Variables, Values, and Operators

Value types:

*   String

    *   Text values

    *   Wrapped with single or double quotes

    *   Can also be created with backticks (\`)

*   Number

    *   Positive or negative

    *   With decimal point (float) or without it (integer)

*   Boolean

    *   True or false

    *   A simple "yes" or "no" value type

    *   Typically used in conditions

*   Null & undefined

    *   "There is no value"

    *   undefined: default if no value was assigned yet

    *   null: explicitly assigned by developer (reset value)

Rules and recommendations for variables/identifiers:

*   Must not contain whitespace or special characters (except \$ and \_ )

*   May contain numbers but must not start with a number

*   Must not clash with reserved keywords

*   Should use camelCasing

*   Should describe what the thing it identifies contains or does

Variables can be delcared using `let` or `const`, but `const` can't be changed once it's assigned. It's good practice to use `const` whenever possible for values that should not be reassigned.

#### Operators:

*   `+` for adding numbers and concatenating strings

*   `*` for multiplication

*   `-` for subtraction

*   `/` for division

*   `=` for assignment

*   `===` for comparing values. An expression comparing two values with this operator will return `true` if the values are equal.

*   `>` for "greater than"

*   `>=` for "greater than or equal to"

*   `<` for "less than"

*   `<=` for "less than or equal to"

### Functions

Function syntax options:

```javascript
function greet1(){
  console.log("Hello!"); 
}

const greet2 = () => {
  console.log("Hello!"); 
]
```

The arrow notation is especailly popular for *anonymous* functions, or functions that have no name.

Arrow notation notes and shortcuts:

*   If your arrow function takes **exactly one parameter**, you may omit the wrapping parentheses.
    So instead of: `(userName) => { ... }`
    You can use: `userName > { ... }`
    **Note:** If your function takes **no parameters** *OR* **more than one parameter**, parentheses **must be included**

*   If your arrow function contains **no logic but a `return` statement,** you can omit the curly braces and the `return` keyword.
    Instead of:

    ```javascript
    number => {
    return number * 3
    }
    ```

    You can use: `number => number * 3;`
    Note that the `return` keyword is not used. `number => return number * 3;` would be invalid.

*   The previous bullet has special rules when attempting to return an object. So for:
    `number => { age: number };  // trying to return an object.`
    JavaScript interprets the content of the curly braces as **function body wrappers**, not as a shorthand for a return statement with an object. To make the object creation explicit, wrap it in parentheses:
    `number => ({age: number});`

### Objects

Basic object syntax:

```javascript
const user = {
  name: "Joe", 
  age: 36, 
  greet() {
    console.log('Hello, ' + this.name + '!') 
  }
}
```

Classes are object blueprints. To create a class:

```javascript
class User {
  constructor(name, age) {
    this.name = name; 
    this.age = age; 
  }
  greet() {
    console.log('Hi!'); 
  }
}

const user1 = new User("Joe", 36); 
```

A constructor is a special function that executes when an instance of that class is created. The constructor can accept defined parameters and set the object's initial values.

### Arrays

Basic array syntax:

```javascript
const hobbies = ["Sports", "Cooking", "Reading"]; 
console.log(hobbies[1])  
```

Arrays have a lot of utility functions, like `findIndex()`, which accepts a function parameter that it executes on every item in the array until one of the values evaluates to "true." Once a match is found, the index is returned. 
```javascript
const itemIndex = hobbies.findIndex((item) => {
  return item === 'Sports'; 
})

// This can be simplified because the only thing in the function body is a `return` statement. 

const index = hobbies.finxIndex ((item) => item === "Sports");
```

The `map()` method allows you to transform every item in an array. Like `findIndex()`, it takes a function as a parameter, and it returns a new array that contains the transformed values. 
```javascript
const editedHobbies = hobbies.map((items) => item + "!"); 
```
Note: Map can also be used to build an array of objects with the values from an array. When doing this, wrap the curly braces in parentheses. As we saw with the return statement shorthand, JavaScript will interpret the curly braces as function body wrappers. Adding the parentheses wrapper around the curly braces indicates that they're defining an object. E.g.
```js
const editedHobbies = hobbies.map((item) => ({text:item})); 
//Returns an array containing 1 object for each hobby. 
// [ {text: "Sports"}, {text: "Cooking"}, {text:"Reading"}]
```

### Control Structures
#### Destructuring Arrays
**Destructuring** an array refers to using a specific syntax to shorten and simplify the extraction of data from the array. 

```js
// Old way of getting values from an array
const userNameData = ["Joe", "Bosh"]; 
const firstName = userNameData[0]; 
const lastName = userNameData[1]; 

// With destructuring 
const [firstName, lastName] = ["Joe", "Bosh"]; 
```
The variables are created and assigned to a new or existing array as long as the defined array (to the left of the `=`) matches the array structure. 

#### Destructuring Objects
```js
// Old way: 
const user = {
  name: "Joe", 
  age: 36
}
const name = user.name; 
const age = user.age; 

// With destructuring 
const {name, age} = {
  name: "Joe", 
  age: 36
}
```
**Important:** When destructuring an object, you **must** use variable names that match the keys defined in the object. To define your own aliases, you must specify the key they're referencing, not just the position they're in (like with arrays). E.g. 
```js
const {name: userName, age: userAge} = {
  name: "Joe",
  age: 36
}
```
#### Destructuring Function Parameters
Destructuring can be used for function parameters that will contain objects. The parameter will be destructured to pull out the object properties and make them available as locally scoped variables. E.g. 
```js
// Without destructuring: 
function storeOrder(order){
  localStorage.setItem('id',order.id); 
  localStorage.setItem('currency', order.currency); 
}
// With destructuring 
function storeOrder({id, currency}) {
  localStorage.setItem('id', id); 
  localStorage.setItem('currency', currency); 
}

// Function call: 
storeOrder({id: 5, currency: 'USD', amount: 15.99}); 
```
Note that the `storeOrder()` function still only takes a single object as a parameter. 

#### Spreading Arrays
The spread operator (`...`) can be added to the beginning of a variable containing an array to refer to the items inside the array. This is useful for combining arrays. E.g. 
```js
const colors = ['Red', 'Blue', 'Green']; 
const moreColors = ['Yellow', 'Orange', 'Purple']; 

const allColors = [...colors, ...moreColors]; 
```
`allColors` will contain all the string values from each of the member arrays. 

#### Spreading Objects 
Spread operator applied to objects: 
```js
const user = {
  name: 'Joe', 
  age: 36
}

const extendeduser = {
  isAdmin: true, 
  ...user
}
```
The spread operator will extract the key-value pairs from the `user` object and add them as key-value pairs for the `extendedUser` object. 

#### For/Of Loops
JavaScript now supports the following syntax for looping through arrays: 
```js
const hobbies = ["Eating", "Shidding", "Internet"]; 

for (const hobby of hobbies){
  //
}
```

### Essential Features Used by React
#### Functions as Values
When passing a function into another function as an argument, the parameter function can either be defined in advance and referenced or created as an anonymous function. If defining in advance and referencing in the function call, do not include parentheses after the function name. 

By omitting the parentheses, the function itself is passed in as a value. If the parentheses were included, the function would simply execute. 

Example: 
```js
const handleTimeout = () => {
  console.log("Timed out!"); 
}

// A
setTimeout(handleTimeout, 1000); 
// vs. B
setTimeout(handleTimeout(), 1000); 
```
The `setTimeout()` function expects to receive a function for its first argument. To do this, the function must be passed in *as a value*, which is what's happening in example A above. In example B, `handleTimeout()` executes immediately, and since it doesn't return anything, `setTimeout()` gets nothing for its first argument. 

You can also create functions that accept functions as parameters.
```js
function greeter(greetFn) {
  // Because greetFn stores the function as a value, we can execute it simply by invoking it with the parameter name. 
  greetFn(); 
}

// Here, we're passing in an anonymous function that just logs "Hi" to the console.
greeter(() => console.log("Hi")); 
```

## React Essentials 
### Component Basics 
Components are UI building blocks. React apps are made up of components. React components are rendered with **JSX**, an extension that provides support for HTML-like syntax in JavaScript. JSX code is not natively supported by browsers, and React transpiles the JSX code into JavaScript. 

In React, a component is really just a JavaScript function that follows 2 important rules: 
- The function name must start with an uppercase character
  - Multi-word names should be written in PascalCase (e.g., "MyHeader")
  - Pick a name that describes the UI building block (e.g., "Header", or "MyHeader")
- The function must return a renderable value
  - In most cases, JSX is returned. 
  - Also allowed: string, number, boolean, null, array of allowed values 

Example: 
``` JSX
function App() {
  return (
    <div>
      <header>
        <img src="src/assets/react-core-concepts.png" alt="Stylized atom" /> 
        <h1>React Essentials</h1> 
        <p>
          Fundamental React concepts you will need for almost any app you are going to build! 
        </p> 
      </header>

      <main>
        <h2>Time to get started!</h2> 
      </main>
    </div>
  );
}

export default App; 
```

Despite being functions, React components are added to a page in the JSX code by wrapping them in `<` and `>` characters like HTML elements. From this, we can infer that the HTML-like JSX tags (`<div>`, `header`, etc) are themselves components and JavaScript functions. Max sometimes refers to these as "built-in" components and contrasts them with "custom" components. 

Built-in: 
- Name starts with a lowercase letter ("body", "header") 
- Only valid, officially defined HTML elements are allowed
- Are rendered as DOM notdes by React. 

Custom: 
- Name starts with an uppercase character 
- Defined by the developer, "wraps" built-in or other custom components 
- React "traverses" the component tree until it has only built-in components left. 

Adding to the code above, the content in the `<header>` element could be made into its own component. This would usually happen in its own file, but it's combined here for simplicity. 

```jsx
function Header() {
  return (
    <header>
      <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
      <h1>React Essentials</h1> 
      <p>
        Fundamental blah blah blah
      </p>
    </header>
  ); 
}

function App() {
  return (
    <div>
      <Header /> 
      <main>
        <h2>Time to get started!</h2> 
      </main>
    </div>
  )
}
```

You may sometimes come across React projects that use JSX code even though the file extension is `.js`. The underlying build process in React can be configured to handle these files properly. 

### Using & Outputting Dynamic Values 
Curly braces `{}` can be used to insert dynamic values into a component. E.g. 

```jsx
const reactDescriptions = ['Fundamental', 'Crucial', 'Core']; 

function getRandomInt(max) {
  return Math.floor(Math.random() * (max + 1)); 
}

function Header() {
  return (
    <header>
      <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
      <h1>React Essentials</h1> 
      <p>
        {reactDescriptions[getRandomInt(2)]} blah blah blah
      </p>
    </header>
  ); 
}
```

To simplify even further, store the ugly part in a variable and render the variable. E.g. 
```jsx
const description = reactDescriptions[getRandomInt(2)];
// ... 
{description} blah blah blah
```

### Setting HTML Attributes Dynamically and Loading Image Files 
Referencing a local image file path in the `src` attribute of an `img` JSX element is not recommended. Instead, use an `import` statement to store a reference to the image in a variable, and pass the variable into the `img` JSX element. E.g. 

```jsx
import reactImg from './assets/react-core-concepts.png'; 
// The variable, reactImg, can be anything 
// ... 
return (
  <header>
    <img src={reactImg} />
    // Note the absence of quotation marks around the attribute value. 
)
```

### Making Components Reusable with Props 
Data can be passed into components via **props**, which take the form of attributes in the HTML-like syntax of JSX. 

In the example below, the `CoreConcept` component has 3 props, `title`, `description`, and `image`. Instead of passing the 3 parameters into the `CoreConcepts` function, React's component syntax expects and accepts only 1 argument, the `props` object. Below, it's just called `props`, but you can call it whatever you want. 

The contents of the `props` object are determined by the values 

```jsx
import componentsImg from './assets/components.png'; 

function CoreConcept(props) {
  return (
    <li>
      <img src={props.image} alt="..." />
      <h3>{props.title}</h3>
      <p>{props.description}</h3>
    </li>    
  ); 
}

function App() {
  return (
    <div>
      <CoreConcept title="Components" 
                   description="The core UI building block" 
                   image={componentsImg} 
      />
    </div>
  )
}
```

If a component's props match key/value structure of a data object, a shorthand can be used to create the instance of the component. 
```jsx
const CORE_CONCEPTS = [
  {
    title: "Title A", 
    description: "Description A", 
    image: "imageA.png" 
  },
  {
    title: "Title B", 
    description: "Description B", 
    image: "imageB.png" 
  },
]

// Both the CORE_CONCEPTS object and the CoreConcepts component use the same 3 key/value pairs. 
// The long way to do this: 
<CoreConcept 
  title={CORE_CONCEPTS[0].title} 
  description={CORE_CONCEPTS[0].description} 
  image={CORE_CONCEPTS[0].image} 
/>
// Repeating this can be arduous. As an alternative: 
<CoreConcept {...CORE_CONCEPTS[1]} />
// Where the spread operator extracts the key/value pairs from the object at the specified index of the data array. 
```

The structure of the `props` object can be made clearer by destructuring it in the component delcaration. This also simplifies the syntax within the component itself. 

```jsx
function CoreConcept({image, title, description}) { 
  return (
    <li>
      <img src={image} alt={title} />
      <h3>{title}</h3> 
      <p>{description}</p>
    </li>
  ); 
}
```

If the data you're going to use for props is already stored in a JavaScript object, you can pass that object as a single prop value instead of splitting it across multiple props. 

```jsx
// Doesn't have to be "concept." Can be anything
// To add the component: 
<CoreConcept concept={CORE_CONCEPTS[0]} /> 
// In the CoreConcept component, you'd have access to a single prop object: 
export default function CoreConcept({ concept }) {
  // Use concept.title, concept.description, etc. 
  // Or destructure the concept object: const { title, description, image } = concept; 
}
```

You can also pass multiple props to a component and then, in the component function, group them into a single object via JavaScript's "Rest property" syntax: 
```jsx
// If a component is used like this: 
<CoreConcept
  title={CORE_CONCEPTS[0].title}
  description={CORE_CONCEPTS[0].description}
  image={CORE_CONCEPTS[0].image} />

// You can group the received props into a single object like this: 
export default function CoreConcept({ ...concept }){
  // ...concept groups multiple values into a single object
  // Use concept.title, concept.description etc. 
  // Or destructure the concept object: const { title, decription, image } = concept; 
}
```
Here, Max acknowledges that this syntax is confusing. We'll see more examples of this with more thorough explanations throughout the course. 

Some props may be optional. In that case, you might want to set default values for props in case a value isn't set. This is a simple matter of using the default values syntax supported in JavaScript destructuring: 
```jsx
<Button type="submit" caption="My Button" />
<Button caption="My Second Button" />

export default function Button({ caption, type="submit" }){
  // caption has no default value, type has a default value of "submit" 
}
```

### Component/Project Structure Best Practices 
So far, examples have placed multiple components in a single file. However, best practice in React is to separate these components into their own files to make larger projects easier to manage. 

Typically, the best way to do this is to create a "components" folder within the existing "src" folder. It's customary to name the component file the same thing as the component itself. 

For example, in the file at `/components/Header.jsx`: 
```jsx
export default function Header(){
  // It's important to capitalize the first letter of the component name
  // The export keywould makes the component available outside the file 
  // Customarily, the component function is the default export from the component file, but it doesn't necessarily have to be. 
  // ...
}
```

The `Header` component can then be imported wherever it needs to be used. Because it's the default export from the file, it can be given an alias when it's imported, but that alias must also start with a capital letter. 

### Component Styles 
Typically, component CSS is also stored in its own file, also named to match the component it supports. The CSS file then has to be imported into the component's jsx file. This import statement is simply `import './Header.css';`. Note, however, that separating CSS code into separate files does not limit the scope of that CSS. If an element is styled in one CSS file, even if that file's component isn't on the page, the CSS will still apply to any of those elements that do appear on the page. Later, we'll learn about a solution to this problem. 

Another common practice is to create a subfolder within the components folder that will contain the files for a component that has several. For example, if you have both a jsx file and a css file, it's easier to keep them organized by storing them in a subfolder. 

### The "Children" Prop 
Up to this point, the components we've created have been self-terminating (with a ` />` at the end). Components can also be added to a page with distinct opening and closing tags (e.g. `<Header></Header>` instead of `Header />`). The content between the opening and closing tags will not be rendered on the page (because the component file is what determines what's rendered), but it is stored in the `children` prop. 

For example: 
```jsx
<menu>
  <TabButton>Components</TabButton> 
</menu>
// and in the component file 
export default function TabButton(props){
  return <li><button>{props.children}</button></li>
}
```

The text between the `TabButton` opening and closing tags, "Components," is automatically stored in `props.children`. It can also be accessed by destructuring the `children` property out of the `props` object in the function delcaration (`export default function TabButton({children}){}`). 

This is just another way to pass information from the parent component to the child. Using children vs attributes is partially a stylistic choice, but consider: 
- Using "children" for components that take a **single piece of renderable content**. This approach is closer to normal HTML usage and is especially convenient when passing **JSX code as a value** to another component. 
- Using "attributes" when you are passing **multiple smaller pices of information** to send. Adding **extra props** instead of just wrapping the content with the component tags means **extra work**. 

### Reacting to Events 
React components have several built-in props that can be used as event listeners. For example, the `onClick` prop can trigger on click events and execute a function. There are actually quote a few "on-" event listeners available. Type "on" and press `CTRL` + `SPACE` to bring up the suggestions menu. 

```jsx
export default function TabButton({ children }) {
  function handleClick(){
    console.log('Hello world!'); 
  }

  return (
    <li>
      <button onClick={handleClick}>{children}</button>
      // Note that parentheses are not included with the function
      // `handleClick` is the value of the function
      // `handleClick()` executes the function
    </li>
  )
}
```

When responding to events, make sure to handle the event in the same component that manages the data that should be changed. Basically, this means that if you want to change the content/structure of the current component, the function that does that work must have access to the rest of the code in the component. For example, if you wanted to click a button and change the contents of a menu area, the button must be clicked, but the button component code isn't going to be the ideal place to update the menu area. Instead, it's better to be able to trigger the click event from the menu area component so the entire component structure is available. 

The `onClick` handler (and others like it) are only available to built-in components like `<button>` and `<li>`. Our custom components aren't able to access them. 

Example: 
```jsx
// App.jsx: 
import TabButton from './components/TabButton.jsx';

function App() {
  function handleSelect() {
    console.log('Hello World - selected!');
  }

  return (
    <div>
      <Header />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            <CoreConcept
              title={CORE_CONCEPTS[0].title}
              description={CORE_CONCEPTS[0].description}
              image={CORE_CONCEPTS[0].image}
            />
            <CoreConcept {...CORE_CONCEPTS[1]} />
            <CoreConcept {...CORE_CONCEPTS[2]} />
            <CoreConcept {...CORE_CONCEPTS[3]} />
          </ul>
        </section>
        <section id="examples">
          <h2>Examples</h2>
          <menu>
            <TabButton onSelect={handleSelect}>Components</TabButton>
            <TabButton onSelect={handleSelect}>JSX</TabButton>
            <TabButton onSelect={handleSelect}>Props</TabButton>
            <TabButton onSelect={handleSelect}>State</TabButton>
          </menu>
          Dynamic Content
        </section>
      </main>
    </div>
  );
}

export default App;

// ... 
// TabButton.jsx: 

export default function TabButton({ children, onSelect }) {
  return (
    <li>
      <button onClick={onSelect}>{children}</button>
    </li>
  );
}
```

Takeaways: 
- Because `onClick` isn't available to a custom component, it must be invoked in the body of the `TabButton` component, specifically in the `button` component. 
- The `onClick` used in the `button` component calls a function that is passed into the component by the parent in App.jsx. 
- The `onSelect` attribute of the `TabButton` component takes a function as an argument and just executes it on click. 
- The function accepted by the `TabButton` `onSelect` function is defined in the App.jsx file. This allows the changes to the dynamic content area to be controlled within the App.jsx file as well. 

If you need to pass data into a function call to be used in the component, anonymize the function to make use of additional values and more complex logic: 

```jsx
<TabButton onSelect={() => handleSelect('components')}>Components</TabButton> 
```
Note that the parentheses are added to the `handleSelect` function call because it's no longer be passed in as a value to `onSelect` but rather being executed in the body of the anonymous function that is triggered by `onSelect`. 

By default, React will only execute a React component function 1 time: when it's first encountered. This means that the UI won't be updated to reflect changes to any of the values in the component. So, for example, creating a variable to hold the UI elements of a section and then changing the value of that variable will not trigger the component to rerender and update the value. This is where **state** comes in. 

### Managing State & Using Hooks
`useState` is a React **hook**, as are all functions that start with "use." The `useState` hook is used to manage a component's **state**, a value tracked by React that, when changed, triggers a rerendering of the component. 

Rules for hooks: 
1. Only call hooks **inside of component functions**. React hooks must not be called outside of React component functions. 
2. Only call hooks **on the top level**. React hooks must not be called in nested code statements (e.g. inside if-statements) 

The `useState` hook accepts a single argument, which is the default value that React should use for the state variable. It yields an array with exactly 2 elements: the current state value and the state update function.  
* The current state value refers to whatever the state value is in the current rendering of the component. 
* The state update function updates the state value and triggers the reexecution of the component function. 

The array returned by `useState` can be stored in a `const`, but it's standard practice to destructure it. 

In the example below, the state variable stores the content that should appear in the UI when an associated button is clicked. Every time the button is clicked, the assocaited value is passed into the state update function. The component function executes again, and the value passed into the state update function becomes the current state value that is the first element in the state array returned by the `useState` hook. 

```jsx
import { useState } from 'react'; 

function App() {
  const [ selectedTopic, setSelectedTopic ] = useState('Please click a button'); 

  function handleSelect(selectedButton) {
    setSelectedTopic(selectedButton); 
    // The handleSelect function reacts to the user input (click) and passes the clicked value to the state setter function, which triggers the rerender. 
  }

  return (
    // ...
    {selectedTopic}
    // In the returned JSX, the current value of the state variable is rendered on the page. 
  )
}
```

Important note: the value of `selectedTopic`, or whatever you use for the current state variable, doesn't change immediatley once you call the state update function. For example, if you called the state update function and then immediately logged the current state variable to the console, it would not reflect the updated value you just passed in. That value won't change until the component function executes again. 

In a more advanced example, Max has an array called `EXAMPLES` containing objects that each contain a title, a description, and some example code. Each button value matches the key used in the array for the object. E.g. 'jsx' button matches 'jsx' object with a title, description, and example code. Then, displaying the content on the page is just a matter of accessing the object in the array via the value of the current state: `EXAMPLES[selectedTopic].title`. This causes a problem with the initial value ("Please click a button") that doesn't have a corresponding object in the array. Max just sets it to "component" for the time being. 

The `useState` hook doesn't *have* to have an initially-selected value, meaning that no value needs to be passed into it as an argument. 

### Rendering Content Conditionally 
In previous examples, the page failed to render because the default value of "Please click a button" doesn't have a corresponding object in the `EXAMPLES` array. The solution is to output content conditionally so that nothing appears in the content area until a value is set for `selectedButton` (by clicking a button). 

There are multiple ways for conditionally displaying content. 

#1. Use a ternary operator in curly braces 
```jsx
const [selectedTopic, setSelectedTopic] = useState(); 
// No default value is used. 

return (
  {!selectedTopic ? <p>Please select a topic</p>:null} 
  // Checks whether there's a value for selectedTopic. If so, display the text. If not, display nothing. 
  {selectedTopic ? (
                    <h3>{EXAMPLES[selectedTopic].title}</h3>
                    //...                   
                    ) : null} 
)
// This example can also be consolidated into a single expression. 
```

#2. Use the && operator 
The `&&` operator automatically returns what follows it if what preceeds it is true. 
```jsx
{!selectedTopic && <p>Please select a topic.</p>}
// If the !selectedTopic evaluates to true, which it does initially because it's not given a default value, the paragraph tag content is automatically returned. 
```

Both of these examples do the heavy lifting inside the return statement, which makes it kind of difficult to read. One way to clean it up is to perform the logic before the return statement: 

```jsx
let tabContent = <p>Please select a topic</p>; 
// Note that this doesn't have to be stored in a string. It's recognized by JavaScript as JSX code. 
if (selectedTopic){
  tabContent = (
    <div id="tab-content">
      <h3>{EXAMPLES[selectedTopic].title}</h3>
      // ... 
    </div>
  )
}
// ... 
return (
  //... 
  {tabContent} 
)
```

In this example, the only conditional logic is happening before the return statement. 

### CSS and Dynaming Styling 

In JSX, a class is added to an element using `className` instead of `class` like in typical HTML because `class` is a reserved term in JavaScript. 

```jsx
export default function TabButton({ children, onSelect, isSelected }) {
  console.log("Tab Button Component Executing"); 
  return (
    <li>
      <button className={isSelected ? 'active' : ''} onClick={onSelect} >
        <children> 
      </button> 
    </li>
  ); 
}

// In the parent component, the isSelected prop is added to the TabButton component, and each instance of TabButton has a value for isSelected that evaluates whether that button matches the topic selected by the user. 

// ... 
<TabButton isSelected={selectedTopic === 'components'}>
```

### Outputting List Data Dynamically 
In the examples so far, JSX elements have been added to the page multiple times, a tedious manual process that can be improved. To do this dynamically, use the `map()` method, which takes a JavaScript function that uses an array item as an input: 

```jsx
return (
  // ... 
  {CORE_CONCEPTS.map((conceptItem) => (
    <CoreConcept {...conceptItem} />)}
  )
)
```
While this works, you'll get an alert in dev tools saying that each of these iteams should have a key property. To remove this error, Max just adds `key={conceptItem.title}` to the `CoreConcept` element. React uses the `key`, which must be a unique value, to manage and update the items in the list. 

## React Essentials - Deep Dive 

### Alternatives to JSX & Fragments 
Technically, it's not necessary to use JSX in React. It's also possible to use the `React.createElement` function: 

```jsx
React.createElement(
  'div',
  { id: 'content' },
  React.createElement(
    'p',
    null,
    'Hello World'
  )
); 
```

JSX is a lot easier to read/write, though. 

When returning a JSX value in a functional component, the JSX element must be rooted in a single "parent" element, like a div. If instead multiple sibling elements are returned, an error will occur. This is rooted in JavaScript, where functions cannot return multiple values. In JSX syntax, multiple sibling elements are interpreted as multiple values, so the sublings must be wrapped in a single parent. 

Wrapping multiple sibling elements in a parent for the return statement works, but it creates an unnecessary element on the page. To avoid this, React provides a `Fragment` component, which can be imported from React and used as a wrapper. The `Fragment` component allows the sibling elements to be returned without rendering an unnecessary parent element on the page. 

To further simplify, leave the `Fragment` import out and just use empty tags in its place. E.g. 
```TypeScript
return (
  <Fragment>
    <Header /> 
    <main></main> 
  </Fragment> 
)
// Works just as well as 
return (
  <>
    <Header /> 
    <main></main>
  </>
)
```

### When should you split components? 
Generally, components should be split up to keep any one component from becoming too complicated or supporting more than one feature. 

### Prop Accessibility in Inner Elements 
When setting an ID on a custom component, remember that it doesn't work the same way as it does in HTML. For example, assigning an ID to a custom component will not automatically apply that ID to the JSX code returned by that component. 

``` JSX
<MyComponent id="examples" />
// *** 
export default class MyComponent({title}){
  return (
    <section>
      {title}
    </section>
  )
}
// In a JSX element, the ID assignment is sending a value to the component as a prop, not assigning a value to the rendered HTML code. 
// But since there's nothing in the component's code catching the ID prop, nothing happens with it. 
// One possible way of resolving this is to have the component catch the prop and assign it to a non-custom component's ID attribute: 

export default function MyComponent({title, id}){
  return (
    <section id={id}>
      {title}
    </section> 
  )
}
// This technically works. The problem, however, is that this gets tedious and unsustainable as more attributes are needed for more child elements. 
```

The more scalable solution is to forward extra props by grouping them together in a single identifier preceded by 3 dots (`...`). This syntax wraps up anything passed into the component but not explicitly identified in the destructured object.  

> Note: This syntax looks like a spread operator, but it's not the same thing. Note the use of an actual spread operator in the code below, which expands whatever is in the `props` object and adds it to the `section` element. 

``` JSX 
export default function MyComponent({title, ...props}){
  return (
    <section {...props}>
      <h2>{title}</h2> 
    </section>
  )
}
```

To take this a step further, if you know that your custom component is using elements that have a certain built-in event handler (like the `onClick` handler in a `button` element), you can assign a value directly to the event handler and forward it to the child elements. 

``` JSX 
<TabButton onSelect={() => handleSelect('components')}>
// ...
export default class TabButton({onSelect}){
  return (
    <button onClick={onSelect}> 
      Button Label
    </button>
  )
}
// becomes 
<TabButton onClick={() => handleSelect('components')}>
// ...
export default function TabButton({...props}){
  return (
    <button {...props}>
      Button Label
    </button>
  )
}
```
Because `onClick` works with the `button` element, we can save a step by just assigning a value to it in `TabButton` and destructuring `props` in the returned `button`. 

### Working with Multiple JSX Slots 
The `children` prop allows a component to access the elements nested within it, but what if additional (but distinctly separate) JSX code is needed to be passed in as well? It's common practice in React to pass JSX code into any prop, and sometimes this is necessary in order to maintain access to certain properties in the parent component. 

``` JSX
export default function MyComponent(){
  return (
    <ComponentA extraSlot={
      <>
        <ComponentB />
        <ComponentB />
      </>
    }>   
      <ComponentC />
      <ComponentC /> 
    </ComponentA>
  )
}
// ... 
export default function ComponentA({children, extraSlot}){
  return (
    // ...
    // the "children" prop will contain the ComponentC instances
    // The "extraSlot" prop will contain the ComponentB instances 
  )
}
```

### Setting Component Types Manually 
Another common practice in React is to dynamically set an element type (technically a component type) by passing the name of the element into a prop. 

E.g. 
``` JSX
<ComponentA buttonWrapper="menu"> 
  <>
    <button>Button A</button>
    <button>Button B</>
  </>
</ComponentA>
// ...
export default function ComponentA({children, buttonWrapper}){
  const ButtonWrapper = buttonWrapper; 
  // This is an important step when dynamically setting a component type. A new variable must be declared, starting with a capital letter, and assigned the appropriate prop. The capital letter is what indicates that it's a custom component. If the prop passed in starts with a capital letter, this step becomes unnecessary. 
  return (
    <ButtonWrapper>{children}</ButtonWrapper>
  )
}
```

> Note: Built-in components can be passed into a prop as a string, but custom components must be passed as a dynamic value using `{}`. 

### Default Prop Values
Default values for props can be assigned right in the function delcaration: 
``` JSX
export default class MyComponent({title, picture, ButtonWrapper='menu'}){
  return (
    // yadda yadda yadda 
  )
}
```

### Coding Exercise Example  
``` JSX
import Button from './Button';
import HomeIcon from './HomeIcon';
import PlusIcon from './PlusIcon';

function App() {
  return (
     <div id="app">
      <section>
        <h2>Filled Button (Default)</h2>
        <p>
          <Button>Default</Button>
        </p>
        <p>
          <Button mode="filled">Filled (Default)</Button>
        </p>
      </section>
      <section>
        <h2>Button with Outline</h2>
        <p>
          <Button mode="outline">Outline</Button>
        </p>
      </section>
      <section>
        <h2>Text-only Button</h2>
        <p>
          <Button mode="text">Text</Button>
        </p>
      </section>
      <section>
        <h2>Button with Icon</h2>
        <p>
          <Button Icon={HomeIcon}>Home</Button>
        </p>
        <p>
          <Button Icon={PlusIcon} mode="text">
            Add
          </Button>
        </p>
      </section>
      <section>
        <h2>Buttons Should Support Any Props</h2>
        <p>
          <Button mode="filled" disabled>
            Disabled
          </Button>
        </p>
        <p>
          <Button onClick={() => console.log('Clicked!')}>Click me</Button>
        </p>
      </section>
    </div>
  );
}

export default App;

// The Button component is meant to be flexible, applying CSS classes to elements, among other things. 

export default function Button({children, mode = "filled",Icon, ...props}) {
 let classNames = `button ${mode}-button`; 
 if (Icon){
     classNames += " icon-button";
 }
 return (
     <button className={classNames} {...props}>
     <!-- This section wsa the tricky part for me 
     The Icon component is only used for 2 of the buttons, so the syntax below checks whether there's a value passed in for the Icon component, and renders it if so. 
     -->
    {Icon && (
        <span className="button-icon">
            <Icon />
        </span>
        )}
        <span>
            {children}
        </span>
     </button>
    )
}
```

### Best Practice: Updating State Based on Old State Correctly
When updating the value of a state variable using the `useState` hook and setter function, particularly when using the current value to calculate the new one (like inverting a boolean value), there's a React-specific syntax to follow. Using an exclamation point to invert a boolean value is specifically discouraged because of the way that React schedules updates. 

Refer to the `toggleEditing` function below: 

``` JSX
export default function Player({ name, symbol }) {
  const [isEditing, setIsEditing] = useState(false);

  function toggleEditing() {
    // In JavaScript, the easiest way to invert a boolean value like isEditing is to use an exclamation point before it: 
    setIsEditing(!isEditing);
    // However, because of the way React schedules state updates, this is not recommended. When the state setter function is called, the execution is "scheduled" for some time in the future. It doesn't happen instantaneously (though practically, it probably does happen within a few milliseconds), so it's important to write this in such a way that the state variable's latest value is recognized. This is the recommended syntax: 
    setIsEditing ((editing) => !editing); 
    // In this syntax, instead of using the state variable declared in the useState invocation, you define another variable ("editing") into which React stores the guaranteed-latest value of the state variable. 
  }

  let playerName = <span className="player-name">{name}</span>;

  if (isEditing) {
    playerName = <input type="text" required value={name} />;
  }

  return (
    <li>
      <span className="player">
        {playerName}
        <span className="player-symbol">{symbol}</span>
      </span>
      <button onClick={toggleEditing}>{isEditing ? "Save" : "Edit"}</button>
    </li>
  );
}
```

### Best Practice: Updating Object State Immutably 
Objects and arrays (which are technically objects) are **reference values** in JavaScript. Therefore, it's better to not mutate (i.e. update) them directly. Instead, create a copy and update the copy. 

Wrong: 
``` JSX
const updatedUser = user; 
user.name = 'Joe'; 
// Because user is an object, this method changes the object in memory. 
```

Right: 
``` JSX
const updatedUser = { ...user };
updatedUser.name = 'Joe'; 
// Editing the copy, not the original. 
```

This is particularly important here because of the potential for bugs or unpredictable behavior, espeically if your application is updating the state in multiple places. Editing the state object directly is never a good idea; that's what the setter function is for, and you need a similar but distinct object (and reference value) to pass into that setter function. 

> Deep Dive: reference vs primitive values: https://academind.com/tutorials/reference-vs-primitive-values 

A more complex example: 
``` JSX
const initialGameBoard = [
  [null, null, null], 
  [null, null, null], 
  [null, null, null]
]; 

const [gameBoard, setGameBoard] = useState(initialGameBoard); 

function handleSelectSquare(rowIndex, colIndex){
  setGameBoard((prevGameBoard) => {
    // At first glance, it looks like the right path is to do this: 
    // const updatedBoard = [...prevGameBoard]
    // However, prevGameBoard still contains 3 arrays (which are objects in JavaScript) that are memory references, so they have to be remapped the same way prevGameBoard does. 
    const updatedBoard = [...prevGameBoard.map(innerArray => [...innerArray])]; 
    // This way, updatedBoard is a new array containing 3 new arrays that all hold the same values as the original. 
  })
}
```

### Core Concept: Lifting State Up
Honestly, Max's definition of this was a little unclear, so the following definition is from React's official documentation: 

*Sometimes, you want the state of two components to always change together. To do it, remove state from both of them, move it to their closest common parent, and then pass it down to them via props. This is known as lifting state up, and it’s one of the most common things you will do writing React code.*

> Note: Concatenating strings in JavaScript is much easier using backticks, a dollar sign, and curly braces, known as **template literal** syntax. E.g. `` `${obj1.key}${obj2.key}`  ``

In Max's example project (the Tic-Tac-Toe game), the App component contains a Player component and a Gameboard component. The Player component is added to the app twice (once for each player), and the Gameboard is added once. Both components need to know whose turn it is, but for different reasons: 
* The Player component must be able to identify whose turn it is by drawing a box around that player using a CSS class. 
* The Gameboard component must know which symbol to add to the box (either "X" or "O") when a box is clicked. 
  * The Gameboard component must also be prepared to respond to user input (clicking a box) to make a move. 

Because both components need this information, it is managed in the App component: 

``` JSX
function App() {
  // activePlayer is the state that has been "lifted up" to the nearest ancestor of the two dependent components, Player and Gameboard 
  const [activePlayer, setActivePlayer] = useState("X");

  // handleSelectSquare is called when it's time to switch turns. It's defined in the App component, but it is sent down to the Gameboard component, which will trigger it in response to a button click. That button lives inside the Gameboard, not the App. 
  function handleSelectSquare() {
    // Remember, when calling the state setter function, you can pass in a function that accepts 1 argument (by default, the current state value) and returns the new state value.
    // In this case, the new state value is dependent on the current state value. 
    setActivePlayer((curActivePlayer) => (curActivePlayer === "X" ? "O" : "X"));
  }

  return (
    <main>
      <div id="game-container">
        <ol id="players" className="highlight-player">
        <!-- 
        The default value of activePlayer is "X" because X will always go first. However, as the state is updated, the CSS needs to be updated as well. Because activePlayer holds a value of either X or O, the comparison is simple, and an isActive prop is defined for the Player component to determine whether that Player component represents the current player's turn. 
        -->
          <Player
            initialName="Player 1"
            symbol="X"
            isActive={activePlayer === "X"}
          />
          <Player
            initialName="Player 2"
            symbol="O"
            isActive={activePlayer === "O"}
          />
        </ol>
        <!-- 
        To access the handleSelectSquare function in the Gameboard component, it needs to be passed in as a prop. 
        -->
        <GameBoard onSelectSquare={handleSelectSquare} />
      </div>
    </main>
  );
}
// In Gameboard.jsx: 
const initialGameBoard = [
  [null, null, null],
  [null, null, null],
  [null, null, null],
];

// Destructing syntax is used to create the onSelectSquare prop that carries the handleSelectSquare function. 
export default function GameBoard({ onSelectSquare }) {
  let gameBoard = initialGameBoard;
  const [gameBoard, setGameBoard] = useState(initialGameBoard);

  // This gets pretty confusing, because we're reusing a term (handleSelectSquare) here
  // This function is called when a box is clicked (note the onClick listener attached to the button below)
  // In addition to performing other functions (like calling another state setter function for the Gameboard), this function calls onSelectSquare, the function passed down from the App component. This function's execution will trigger an update to the activePlayer state variable. 
  function handleSelectSquare(rowIndex, colIndex) {
    setGameBoard((prevGameBoard) => {
      const updatedBoard = [
        ...prevGameBoard.map((innerArray) => [...innerArray]),
      ];
      updatedBoard[rowIndex][colIndex] = activePlayerSymbol;
      return updatedBoard;
    });
    onSelectSquare();
  }

  return (
    <ol id="game-board">
      {gameBoard.map((row, rowIndex) => (
        <li key={rowIndex}>
          <ol>
            {row.map((playerSymbol, colIndex) => (
              <li key={colIndex}>
                <button onClick={() => handleSelectSquare(rowIndex, colIndex)}>
                  {playerSymbol}
                </button>
              </li>
            ))}
          </ol>
        </li>
      ))}
    </ol>
  );
}

// In Player.jsx: 
// Note: some code has been removed from this component because it's not relevant to the current concept. 
export default function Player({ initialName, symbol, isActive }) {
  return (
    // The logic has already been worked out in the App component. Here, it's only necessary to evaluate the value of isActive. If it's true, the "active" CSS class is applied to the component. Otherwise, the className "attribute" is undefined. The "active" CSS class is what draws the border around the active player. 
    <li className={isActive ? "active" : undefined}>
      <span className="player">
        {editablePlayerName}
        <span className="player-symbol">{symbol}</span>
      </span>
      <button onClick={toggleEditing}>{isEditing ? "Save" : "Edit"}</button>
    </li>
  );
}
```

## Avoding Intersecting States 
In the next stage of the Tic-Tac-Toe project, the log needs to be added. This will be its own component, but it presents a problem with the way state is currently managed. 

The Log component must show a list of each move taken by each player as it happens. Each of these is called a turn, and it makes sense that it would be a custom object that stores a reference to the box clicked by the player and that player's symbol (either X or O, stored in the "activePlayer" state variable). The game's log, therefore, will be an array of turn objects. 

Note, however, that the Gameboard component is already keeping track of some turn information as it happens. When a square is clicked, that square's row index and column index values are passed to the handleSelectSquare function and combined with the activePlayer to determine which symbol goes where. The Gameboard component is then rerendered to reflect the newest move. The Log component could make use of this information, but it also needs to know the order in which the moves occurred. 

We could create an entirely new state object for the Log and manage it separately from the Gameboard state, but this is duplicative. Wherever possible, we should avoid managing the same information in two different states, also known as "intersecting state." Instead, we can lift up the state from Gameboard, manage it in the App component in a way that keeps track of the order of the moves (which is only important for the Log component, not so much the gameboard itself) and make the information available to both the Gameboard and Log. 

In the App component, we create a new state object to hold each turn in the game. This will be an array of "turn" objects, and it is empty by default. 
In the Gameboard component, we remove the handleSelectSquare function altogether. Its purpose was to create a new gameboard object (the multidimensional array) that reflects the most recent move, pass that into the state setter function, and then call function that had been passed into the Gameboard component by the App component as a prop to update the activePlayer. However, we don't need any of this anymore since we'll be rendering the gameboard a slightly different way, using the turns passed in from the App component. This entire function, therefore, can be removed, and the button's onClick event listener can directly call the prop function, now passing in the row index and column index that we'll need in the App component. 

``` JSX 
// In App.jsx:
function App() {
  // gameTurns is used in Gameboard and Log
  const [gameTurns, setGameTurns] = useState([]);
  // activePlayer is used in Player and Gameboard 
  const [activePlayer, setActivePlayer] = useState("X");

  // handleSelectSquare is passed down to Gameboard, attached to the button onClick listener, and called using the rowIndex and colIndex associated with the clicked square. 
  function handleSelectSquare(rowIndex, colIndex) {
    setActivePlayer((curActivePlayer) => (curActivePlayer === "X" ? "O" : "X"));
  
    setGameTurns((prevTurns) => {
      let currentPlayer = "X";

      // This logic checks to see if there are any turns in the array yet (which there won't be on first render) and then sets the currentPlayer based on the first item in the turns array. Note that the newest turn is added as the first item in the array, so the most recent turn is always at index 0. 
      if (prevTurns.length > 0 && prevTurns[0].player === "X") {
        currentPlayer = "O";
      }
      // The structure of the "turn" object is defined here and populated now that all the information is available. 
      const updatedTurns = [
        {
          square: {
            row: rowIndex,
            col: colIndex,
          },
          player: currentPlayer,
        },
        // The remaining items in the array are added after the first item, using the spread operator. 
        ...prevTurns,
      ];
      return updatedTurns;
    });
  }

  return (
    <main>
      <div id="game-container">
        <ol id="players" className="highlight-player">
          <Player
            initialName="Player 1"
            symbol="X"
            isActive={activePlayer === "X"}
          />
          <Player
            initialName="Player 2"
            symbol="O"
            isActive={activePlayer === "O"}
          />
        </ol>
        <!-- The turns array is passed into the Gameboard component so it can be used to populate the moves already taken -->
        <GameBoard onSelectSquare={handleSelectSquare} turns={gameTurns} />
      </div>
      <!-- The turns are also passed to the Log component so they can be written out below the board. -->
      <Log turns={gameTurns} />
    </main>
  );
}

// In Gameboard.jsx: 
const initialGameBoard = [
  [null, null, null],
  [null, null, null],
  [null, null, null],
];

export default function GameBoard({ onSelectSquare, turns }) {
  let gameBoard = initialGameBoard;

  // The method of rendering the gameboard is changed here to use the turns array. 
  // Note the use of destructring to define the variables using the arguments passed into the function call 
  // This loop is an example of deriving state from props. Instead of creating a state object in Gameboard, we're using information in the turns array to infer what we need. 
  for (const turn of turns) {
    const { square, player } = turn;
    const { row, col } = square;
    gameBoard[row][col] = player;
  }
  
  return (
    <ol id="game-board">
      {gameBoard.map((row, rowIndex) => (
        <li key={rowIndex}>
          <ol>
            {row.map((playerSymbol, colIndex) => (
              <li key={colIndex}>
                <!-- 
                Before, the onClick listener called a local function that, among other things, called onSelectSquare. Now, the rest of that function isn't necessary, and onSelectSquare can be called directly. 
                Note, however, that we can't just write onClick={onSelectSquare(rowIndex, colIndex)}
                The anonymous function syntax must be used so we can pass arguments in 
                -->
                <button onClick={() => onSelectSquare(rowIndex, colIndex)}>
                  {playerSymbol}
                </button>
              </li>
            ))}
          </ol>
        </li>
      ))}
    </ol>
  );
}

// In Log.jsx: 
export default function Log({ turns }) {
  return (
    <ol id="log">
      {turns.map((turn) => (
        <!-- 
        Remember, the list item has to have a key value. 
        This is always true when outputting a dynamic list 
        -->
        <li key={`${turn.square.row}${turn.square.col}`}>
          {turn.player} placed at row {turn.square.row} column {turn.square.col}
        </li>
      ))}
    </ol>
  );
}
``` 

### Reducing State Management and Identifying Unnecessary State
Deriving values and information from state is a great way to reduce the total number of state objects in your code and make it less complex. 

For example, in App.js: 
``` JSX
// This function can be used both to determine the active player and to handle the selection of a new square (in the handleSelectSquare function) 
function deriveActivePlayer(gameTurns) {
  let currentPlayer = "X";

  if (gameTurns.length > 0 && gameTurns[0].player === "X") {
    currentPlayer = "O";
  }

  return currentPlayer;
}

function App() {
  // The activePlayer state is no longer needed, because we can use the gameTurns array to infer that information. 
  const [gameTurns, setGameTurns] = useState([]);

  const activePlayer = deriveActivePlayer(gameTurns);

  function handleSelectSquare(rowIndex, colIndex) {
    setGameTurns((prevTurns) => {
      let currentPlayer = deriveActivePlayer(prevTurns);

      // Note that the updatedTurns array is adding the turns
      // in the reverse order in which they occur. The most recent
      // turn becomes the first item in the array.
      const updatedTurns = [
        {
          square: {
            row: rowIndex,
            col: colIndex,
          },
          player: currentPlayer,
        },
        ...prevTurns,
      ];
      return updatedTurns;
    });
  }
  // return statement goes here, but no necessary in this example. 
}

```