# jsx syntax

## return
* Alway put the parent opening tag on the same line as the `return` 
```jsx
// ❌
return 
    <main>
    </main>

// ✅
return <main>
        </main>
```
* Or we can wrap up the HTML into a parenthesis
```jsx
return (
    <main>
    </main>
)
```

## Fragment
The Fragment will not be showned up in the root div. So it is sibling elements directly under the div section
```jsx
import { Fragment } from "react"

root.render {
    <Fragment>
        <header></header>
        <main></main>
    </Fragment>
}
```
We can also just skip the Fragment and use <> instead
```jsx
root.render {
    <>
        <header></header>
        <main></main>
    </>
}
```

### ClassName
Because React is turning React element into dom, and in vannila javascript we use `xx.ClassName.add()`, in JSX we should also use `className` instead of class
```jsx
function Header() {
    return (
         <ul className="nav-list">
    )
}
```
- `className=` is an attribute, not a JavaScript expression.
- Curly braces {} in JSX are only for JavaScript expressions (like variables, logic, or calculations).  
- Never put it in the {} like `{props.on ? className="on" : className=""}`
```jsx
export default function Pad(props) {
    console.log(props.on)
    
    return (
        <button 
            style={{backgroundColor: props.color}}
            className={props.on ? "on" : ""}
        ></button>
    )
}
```

## Styles
style prop must be an `object` with `camelCased` property names.
```jsx
import React from "react"
import padsData from "./pads"

export default function App({ darkMode }) {
    const [pads, setPads] = React.useState(padsData)

    const styles = {
        backgroundColor: darkMode ? "#222222" : "#cccccc"
    }

    const buttonElements = pads.map(pad => (
        <button style={styles} key={pad.id}></button>
    ))

    return (
        <main>
            <div className="pad-container">
                {buttonElements}
            </div>
        </main>
    )
}
```


## render an array of jsx element
React can't render an regular object, but it can render an `array` of jsx element.
```jsx
export default function App() {
    const ninjaTurtles = [
        <h2>Donatello</h2>, 
        <h2>Michaelangelo</h2>,
        <h2>Rafael</h2>,
        <h2>Leonardo</h2>
    ]
    return (
        <main>
            {ninjaTurtles}
        </main>
    )
}
```