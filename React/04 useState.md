# State
- State gives us opportunities to maintain data between rerenders of React and cause rerender in React.   
- The UI should be a function of state. React’s approach is not "Manually manipulate the DOM and change things directly." Instead, it is
"Update the state, and let React automatically rerender the UI based on that state."
```jsx
const [isLoggedIn, setIsLoggedIn] = useState(false)

return (
  <div>
    {isLoggedIn ? <Dashboard /> : <Login />}
  </div>
)
```
- If the value of a **local variable** changes, no code will be re-run.   
- When the value of `state` changes and the setter function is called, React will re-render the component which contains the states. 
* Simply modifying the state value directly will not trigger the re-render, and we should `never change a state without a setter function`!


## Import 
There are 2 ways to import useState: 
### Import the default export and give it a name as React
```jsx
import React from "react"

React.useState()
```
- This is the React variable
```jsx
const React = {
    useState: function() { ... },
    useEffect: function() { ... }
}
```

### Import a destructured useState hook from the React library 
```jsx
import { useState } from "react"

useState()
```
- Destructuring means we 
```jsx
const obj = { name: "Tom", age: 18 }
const { name } = obj
```
- So we are doing the same thing
```jsx
const { useState } = React
```
- That is how we get 
```jsx
import { useState } from "react"
```

## useState()
- use `useState()` to create a state
- Without passing in any parameter, it will return an `array`, whose 1st element is **undefined**, and 2nd element is a function. 
```jsx
import React from "react"
const result = React.useState()
console.log(result)
>>> [undefined, ƒ()]
```
When we pass in a value when calling the useState, it provides an **initial state**. 
```jsx
import React from "react"
const result = React.useState("yes")
console.log(result)
>>> ["yes", ƒ()]
```

## useState() array destructure
```jsx
import React from "react"

export function App() {
    // Theoretically We can give whatever name we want to the array destructuring element, but there's a convention
    const [isImportant, setIsImportant] = React.useState("Yes")

    return (
        <main>
            <h1 className="title">Is state important to know?</h1>
            <button className="value">{isImportant}</button>
        </main>
    )
}
```

## Change state
```jsx
import React from "react"

export function App() {
    const [isImportant, setIsImportant] = React.useState("Yes")

     // Run the function will update the State to the new value and re-run the code
    // If we call the function here, it will run again and again ❌ 
    setIsImportance("Definitely!")

    return (
        <main>
            <h1 className="title">Is state important to know?</h1>
            <button className="value">{isImportant}</button>
        </main>
    )
}
```
- The correct way of doing it is to run the `setter function` in a `handle function`.   
- The handle function will only run when some event is triggered.   
```jsx
import React from "react"

export default function App() {
    let [isImportant, setIsImportant] = React.useState("Yes")
    
    function handleClick() {
        setIsImportant("Heck yes")
    }
    
    return (
        <main>
            <h1 className="title">Is state important to know?</h1>
            <button onClick={handleClick} className="value">{isImportant}</button>
        </main>
    )
}
```

## Update a state with callback function
We have 2 options for what you can pass in to a `state setter function`: 
* Pass the new version of state that we want to use as the replacement for the old version of state. Whenever we don't really care about (or need) the old value, we simply want to set a new value.  
* Pass a callback function. Must `return` what we want the new value of state to be.   
    * Use it if we don't directly have the new value, but need to do some modification on the old values to get the new value (need the old value of state to help you determine the new value of state)
    * This callback function will `receive the old value` of state as its `parameter`

```jsx
import React from "react"

export default function App() {
    const [count, setCount] = React.useState(0)

    function add() {
        // setCount(count + 1)
        setCount(prevCount=> prevCount + 1)
    }

    function subtract() {
        // setCount(count - 1)
        setCount(prevCount => prevCount - 1)
    }

    return (
        <main className="container">
            <h1>How many times will Bob say "state" in this section?</h1>
            <div className="counter">
                <button className="minus" onClick={subtract} aria-label="Decrease count">–</button>
                <h2 className="count">{count}</h2>
                <button className="plus" onClick={add} aria-label="Increase count">+</button>
            </div>
        </main>
    )
}
```
## State only take the initial value
When a component re-renders, the state line runs again; However, React only uses the `initial value` the first time the component renders as the state value. 
* In this example, the function generateAllNewDice `will run` every time that the component rerenders
* However, dices will `not be changed` by the new function result in the rerenders. 
```jsx
const [dices, setDices] = useState(generateAllNewDice())
```
* We don't want the function to run so many times.
* In this case, we are passing a `function` to useState, not the `result of the function`.
* On the first render: React sees that the initial state is a function -> React calls that function once -> The returned value becomes the initial state
* On later re-renders: React already has the state stored. So it does NOT call the initializer function again. It simply returns the stored state.
```jsx
const [dices, setDices] = useState(() => generateAllNewDice())
```

## Array state
* We have a list. 
* Click the button the 1st time -> render the 1st element in the list
* Click the button the 2nd time -> render the 2nd element in the list   
......

```jsx
import React from "react"

export default function App() {
    const [myFavoriteThings, setMyFavoriteThings] = React.useState([])
    
    const allFavoriteThings = ["💦🌹", "😺", "💡🫖", "🔥🧤", "🟤🎁"]

    const thingsElements = myFavoriteThings.map(thing => <p key={thing}>{thing}</p>)

    // We should't use the push function because we don't want to change the prevArray!
    function addFavoriteThing() {
        setMyFavoriteThings(prevFavThings => [
            ...prevFavThings, 
            allFavoriteThings[prevFavThings.length]
        ])
    }
    
    return (
        <main>
        <button onClick={addFavoriteThing}>Add item</button>
        <section aria-live="polite">
            {thingsElements}
        </section>
        </main>
    )
}
```

## Object state
```jsx
import React from "react"

const [contact, setContact] = React.useState({
    firstName: "John",
    lastName: "Doe",
    phone: "+1 (212) 555-1212",
    email: "itsmyrealname@example.com",
    isFavorite: true
})

function toggleFavorite() {
    setContact(prevContact => {
        return {
            ...prevContact, 
            isFavorite: !prevContact.isFavorite
        }
    })
}
```

## Local state vs. shared state
Shared state: Set the function in the parent component and pass it down the to the child component 
* We have an array of object concluding the id, color, and on / off of each of the pad.
* For each of the pad, we want to control the on / off  by clicking on it. 
```js
// pads.js
export default [
    {
        id: 1,
        color: "#F18D8B",
        on: true
    },   
    {
        id: 2,
        color: "#F5C280",
        on: false
    },   
]
```
```css
button {
    height: 100px;
    width: 100px;
    border: 3px solid white;
    border-radius: 5px;
    cursor: pointer;   
    opacity: 0.1;
}

button.on {
    opacity: 1;
}
```

### Derived state
* Import the pads data.  
* Map over the array of data, and create pad components.  
```jsx
// App.jsx
import React from "react" 
import pads from "./pads"
import Pad from "./Pad"

export default function App() {
    const padsElement = pads.map(pad => {
        return (
            <Pad 
                key={pad.id}
                color={pad.color}
                on={pad.on}
            />
        )
    })

    return (
        <main>
            <div className="pad-container">
                {padsElement}
            </div>
        </main>
    )
}
```
* For **each of the pad**, create `state` controlling whether this pad is "on" or "off". 
* Pass down a prop called `on` to the pad component, and use the `props.on` to determine the initial state.
* Create an event listener so when the pad is clicked, it toggles from "on" to "off".
```jsx
// Pad.jsx
import React from "react" 

// Set a state for each of the pad
export default function Pad(props) {

    const [toggle, setToggle] = react.useState(props.on)

    function handleClick() {
        setToggle(prevon => !prevon)
    }

    return (
        <button 
            style={{backgroundColor: props.color}}
            className={toggle ? "on" : ""}
            onClick={handleClick}
        >

        </button>
    )
}
```
#### Drawback of derived state
One drawback of derived state is that on the App level, we can't **have a separate button to control the on / off of all the pads.**
* the on / off is controlled by the separate state on each pad level
* on the App level, we can also have a state like this: 
```jsx
// App.jsx

import React from "react"
import pads from "./pads"

export default function App() {
    const [padData, setPadData] = React.useState(pads)
}

```
* However, the `padData` state is not linked to the separate `toggle` state. And it is never rendered. 
* Only the `toggle` state is rendering. 
* So even if we do something like this, it won't work.
```jsx
// App.jsx

import React from "react"
import pads from "./pads"

export default function App() {
    const [padData, setPadData] = React.useState(pads)


    function toggleAll() {
        setPadData(prevPadData => 
            prevPadData.map(pad => 
                {
                    ...pad,
                    on: false
                })
        )
    }
    return (
        <main>
            <div className="pad-container">
                {padsElement}
            </div>
            <button
                onClick={toggleAll}
            >
                Turn off all the buttons
            </button>
        </main>     
    )
}
```
* App re-renders and each Pad receives new props (now on={false}).
* Pad can re-render because its parent re-rendered and its props changed. But the important part is: It re-renders without being `remounted.` 重新安装
* **useState(props.on) doesn’t run again**. useState(initialValue) uses initialValue only on the first mount. After the component is mounted, React ignores that initializer and keeps the stored state value. So this line:
```jsx
const [on, setOn] = React.useState(props.on)
```
* On later renders: React returns the existing on state value (whatever it currently is), not the new props.on
* So after you click “Turn All Off”, props.on becomes false, but local state `on` stays whatever it was before


### Shared state
* Instead of each pad component has its own toggle state, we should go to the App level, and use a `state` there to control all the pad component. 
* On the App level, we will create a toggle function inside of the App.
* We pass the toggle function down to each of the Pad component. When the pad is clicked, it will send the signal (id) to its parent component.
* The toggle function in the App component will update the object of the clicked pad in the array state.

* Now we have an `unified` source of truth. 
```jsx
// App.jsx

import React from "react"
import pads from "./pads"

export default function App() {
    const [padData, setPadData] = React.useState(pads)

    // if item.id (item is each object in the array state) equals to id that is being passed to toggle, we should return the item where the item.on is flipped
    // if it is matched, just resturn the item as it is before
    function toggle(id) {
        setPadData(prevPadData => 
            prevPadData.map(item => 
                item.id === id ? 
                { ...item, on: !item.on} : 
                item
            )
        )
    }

    const padsElement = padData.map(pad => {
        return (
            <Pad 
                key={pad.id}
                id={pad.id}
                color={pad.color}
                on={pad.on}
                toggle={toggle}
            />
        )
    })


    return (
        <main>
            <div className="pad-container">
                {padsElement}
            </div>
            <button
                onClick={toggle}
            >
                Turn off all the buttons
            </button>
        </main>     
    )
}
```
```jsx
// Pad.jsx
import React from "react" 

export default function Pad(props) {

    return (
        <button 
            style={{backgroundColor: props.color}}
            className={props.on ? "on" : ""}
            onClick={() => props.toggle(props.id)}
        >

        </button>
    )
}
```

## Pass data 
- The data can only be passed from the **parents** component to the child component. No child to child (between siblings). No child to parents. 
- In this example, since we got the `state` userName in the Header component, the Body component can never get that state data. 

```jsx
// App.jsx
import React from "react"
import Header from "./Header"
import Body from "./Body"

export default function App() {
    return (
        <main>
            <Header />
            <Body />
        </main>
    )
}
```
```jsx
// Header.jsx
import React from "react"
import avatar from "./icons/user.png"

// We get the state here
export default function Header() {
    const [userName, setUserName] = React.useState("Joe")

    return (
        <header>
            <img src={avatar} />
            <p>{userName}</p>
        </header>
    )
}
```
```jsx
// Body.jsx
import React from "react"

export default function Body() {
    return (
        <section>
            <h1>Welcome back, ___!</h1>
        </section>
    )
}
```
Instead, we should move the state to the parent component. 
```jsx
// App.jsx
import React from "react"
import Header from "./Header"
import Body from "./Body"

export default function App() {
    const [userName, setUserName] = React.useState("Bob")
    
    return (
        <main>
            <Header userName={userName} />
            <Body userName={userName} />
        </main>
    )
}
```