# Basic
JSX = JavaScript XML

React invented it as a syntax that lets you write UI structure (HTML-like) inside JavaScript.  

In a React component file, there are two different zones:

* Normal JavaScript zone
```jsx
const [dices, setDics] = React.useState(generateAllNewDice())
```
* JSX zone: It's anywhere you write HTML-like syntax.
```jsx
<Die value={dice}/>
```

## HTML
```html
	<body>
		<div id="root"></div>
		<script type="module" src="/src/index.jsx"></script>
  	</body>
```
## The process of parsing JSX
1. We write JSX syntax.
```jsx
<div>Hello</div>
```
2. Vite(build tool) turns the JSX syntax(JSX elements) into calls to react.createElement
```js
React.createElement("div", null, "Hello")
```
3. The browser javascript engine run the react.createElement, and react(createElement function) returns **javascript object** as Virtual DOM.
```js
{
  type: "div",
  props: {},
  children: "Hello"
} 
```
4. ReactDOM(library) reads that object and creates real DOM nodes.

5. The browser renders the real DOM.

## react-dom
```jsx
import ReactDOM from "react-dom/client"
import App from "./App"

ReactDOM
    .createRoot(document.getElementById("root"))
    .render(<App />)
```
or another way
```jsx
import { createRoot } from "react-dom/client"

const root = createRoot(document.getElementById("root"))

const reactElement = <h1>Hello from JSX!</h1>

// Vite change jsx syntax into the createElement syntax which creates a js object under the line. 

console.log(reactElement)
>>> {type: 'h1', key: null, props: {children: 'Hello from JSX!'}, _owner: null, _store: {}}

root.render(
    reactElement
)
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

