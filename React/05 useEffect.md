## Side effect
* In React, a side effect is anything a component does that goes beyond returning UI from props and state.
* Example: local storage, API, websockets, DOM manipulation
* Even though a GET request doesn’t modify the server, it still breaks the idea of a “pure render. A GET request is considered a side effect because:
    * It interacts with the outside world (the network).
    * It depends on something React doesn’t control.
    * It can fail, delay, or return different results.
    * It may trigger state updates and re-renders.
* That's why we should put the `side effect` in the `useEffect`

## useEffect
* useEffect is a React Hook that lets you synchronize a component with an `external` system. The function that runs inside the useEffect is the side effect that we created. For example, if we run a call API function inside the useEffect(), the side effect is **call the API**.
* useEffect let other codes run first
```jsx
React.useEffect(()=> {
    console.log("Effect function ran")
}, [])

console.log("Rendered!")

>>> Rendered!
>>> Effect function ran
```

useEffect() has 2 parameters:
* **setup callback function(effect function)**: by default the first parameter will run on every single render
* **optional dependencies array**: it gives us a chance to `stop the function` from running on every single render. It will always be an array of values that React is going to watch between one render and the next.
If any of the values in this array `change` between those two renders, then react will know that it should `run the function again.`
    * if we leave it as an empty array, it means that the `effect function` will only run the first time the `component` mounts to the page

## 1. fetch api request 
```jsx
import React from "react"
import { useParams } from "react-router-dom"

export default function VanDetail() {
    const params = useParams()
    
    React.useEffect(() => {
        fetch(`/api/vans/${params.id}`)
            .then(res => res.json())
            .then(data => console.log(data))
    }, [params.id])
    
    return <h1>Van detail page goes here</h1>
}
```

## 2. Interact with window(browser)
1. For the WindowTracker component, the `useEffect` will only run in the inital render because the independency array is empty. However, when we resize the window, the **browser**(not React) triggers the **event listener** inside the useEffect. The listener calls the setWindowWidth, which triggers the rerender of the component to show the new width. 
2. If we toggle the **Toggle WindowTracker button** on the website many times, and then resize the the screen, we will find that the "Resized" appear many times in the console. Everytime we toggle the component "on", the `useEffect` runs, and it **adds a new event listener** on the window. If we toggle it 10 times, the window now has 10 separate listeners all listening for the resize event.
3. If we won't need to interact with the outside system, we need to clean up any **side effect** that we have created. In this case, we need to remove the event listener. 
```jsx
import React from "react"
import WindowTracker from "./WindowTracker"

export default function App() {

    const [show, setShow] = React.useState(true)
    
    function toggle() {
        setShow(prevShow => !prevShow)
    }

    return (
        <main className="container">
            <button onClick={toggle}>
                Toggle WindowTracker
            </button>
            {show && <WindowTracker />}
        </main>
    )
}
```

```jsx
import React from "react"

export default function WindowTracker() {
    const [windowWidth, setWindowWidth] = React.useState(window.innerWidth)
    
    React.useEffect(() => {
        window.addEventListener("resize", function() {
            console.log("Resized")
            setWindowWidth(window.innerWidth)
        })
    }, [])
    
    return (
        <h1>Window width: {windowWidth}</h1>
    )
}

```

cleanup function
* To clean the side effect when the component unmounts, we can **return** a cleanup function in the useEffect first parameter(the callback function)
    * Toggle On: WindowTracker mounts. Listener #1 is added.
    * Toggle Off: React calls the cleanup function. Listener #1 is removed.
```js
import React from "react"

export default function WindowTracker() {
    const [windowWidth, setWindowWidth] = React.useState(window.innerWidth)

    React.useEffect(() => {

        function watchWindowWidth () {
            console.log("Resized")
            setWindowWidth(window.innerWidth)
        }

        window.addEventListener("resize", watchWindowWidth)
        
        return function() {
            console.log("Cleaning up...")
            window.removeEventListener("resize", watchWindowWidth)
        }
    }, [])

    return (
        <h1>Window width: {windowWidth}</h1>
    )
}
```

## timer
```jsx
const [time, setTime] = React.useState(0)
useEffect(() => {
    setInterval(() => {
        setTime(prev => prev + 1)
    }, 1000)
}, [])

```