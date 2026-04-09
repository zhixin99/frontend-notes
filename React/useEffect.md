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
* useEffect is a React Hook that lets you synchronize a component with an `external` system.
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

## fetch api request 

## cleanup function
* we can `return` a cleanup function in the useEffect first parameter(the callback function)
* It means if the component ever `unmounts`, just run the code that I put inside of this function, 
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