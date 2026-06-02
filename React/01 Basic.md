# Basic
## React
- React is a `library`. It allow us to create easily reusable and interchangeable piece of the web and have various ways of combine together.
- React creates a `virtual DOM` instead of the real DOM. Every time your components render, React updates this lightweight JavaScript copy first, runs its diffing algorithm to see exactly what changed, and then updates the Real DOM (reactDOM) in the browser as efficiently as possible. 

## JSX
- JSX = JavaScript XML
- It is a syntax created by React. It that lets you write HTML-like syntax (not HTML, not s string) inside JavaScript.  
- Before JSX, we need to write React.createElement to create element.  
```js
React.createElement("div", null, "Hello")
```
- In a React component file, there are two different zones:
    - Normal JavaScript zone
    - JSX zone: It's anywhere you write `HTML-like syntax`.
```jsx
const [dices, setDics] = React.useState(generateAllNewDice())
```
```jsx
<Die value={dice}/>
```

## The process of parsing JSX / virtual DOM
1. We write JSX syntax.
```jsx
<div>Hello</div>
```
2. `Vite`(build tool) turns the JSX syntax(JSX elements) into calls to `react.createElement`. 
```js
React.createElement("div", null, "Hello")
```
3. The browser javascript engine run the react.createElement, and `react createElement function` returns **javascript object** as `Virtual DOM.` This simple object is a single Virtual DOM node (often called a React Element). When hundreds or thousands of these objects are nested together in an object tree, that tree is the Virtual DOM.
```js
{
  type: "div",
  props: {},
  children: "Hello"
} 
```
4. `ReactDOM`(library) reads that object and `creates real DOM nodes`.

5. The browser renders the real DOM.

## Create a React file
1. In html file, create a section for the jsx, give it an id of root
```html
<body>
    <div id="root"></div>
    <script type="module" src="/src/index.jsx"></script>
</body>
```
2. Use `react-dom` to transfer the jsx object into real dom and put things into browser.  

```jsx
import ReactDOM from "react-dom/client"

const reactElement = <h1>Hello from JSX!</h1>

// first, it turns your div into a highly optimized React Root Container (createRoot)
const root = ReactDOM.createRoot(document.getElementById("root"))

// then, it hands your app over to that container to manage dynamically (.render
root.render(reactElement)
```

## react
```jsx
// From react(package)，take the default export，and assign it to a variable called React
import React from "react"

console.log(React)
// React is an object variable. 
>>> {
  createElement: f,
  useState: f,
  useEffect: f,
  ...
}
```
```jsx
// Theoretically, We can give it any name, but it is weird so we don't use it. 
import banana from "react" 
```





## Import image
If we are using vite, it will rearrange the code under the hood, compress all the code into a single file, and the structure of the folder may be different, so the relative path may not work.  
```jsx
import mrWhiskerson from "./images/mr-whiskerson.png"
function App() {
    return (
        <div className="contacts">
            <Contact
                img={mrWhiskerson}
                name="Mr. Whiskerson"
                phone="(212) 555-1234"
                email="mr.whiskaz@catnap.meow"
            />
        </div>
    )
}
```

## Template string
Template string is a javascript expression, so we also need to wrap it up in a curly brackets
```jsx
aria-label={`Current answer is ${isGoingOut ? "Yes" : "No"}`}
```

## React component to render markdown
https://www.npmjs.com/package/react-markdown/v/8.0.6#use 
```jsx
import ReactMarkdown from 'react-markdown'
<ReactMarkdown># Hello, *world*!</ReactMarkdown>
```

