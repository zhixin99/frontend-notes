# Routing

## MPA vs. SPA(Single Page Application)
* In MPA, we have several HTML files, and each time a new link is clicked, a new page is rendered; 
* In SPA, when the client request, the server response with a React App, and it is loaded into the browser. When a new request is made, in most cases, portions of the new page can be loaded directly from the **React App**. If it still needs more data or API, a request may still be made out to the server, but the server will only send back some **JSON data** instead of view. 

## Install and setup
```
npm install react-router-dom
```
* BrowserRouter: a context provider.  
* Routes: a smart filter. This **component** looks at the current URL and searches through its children (Route components) to find the best match. It renders only that specific component.
* Route: www.google.com/about -> `/about` is the router. This is where you define the React component you want to show when the path is active. 
    * In JSX, there are two ways to **pass a value to a prop**: 
        * Strings: title="My Projects" (Uses quotes); 
        * **Expressions**: element={<App />} (Uses curly braces)
* Colon mark: A symbol to indicate that there's something here in the URL.
```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom"
import { createRoot } from "react-dom/client"
import Main from "./page/Main"
import About from "./page/About"
import Header from "./component/layout/Header"

function App() {
    return (
        <BrowserRouter>
            <Header />
            <Routes>
                <Route path="/" element={<Main />}/>
                <Route path="/about" element={<About />}/>
                <Route path="/product/:id" element={<ProductDetails />}>
            </Routes>
        </BrowserRouter>
    )
}
createRoot(document.getElementById("root")).render(
    <App />
)
```

## Link
`<Link>` tells React Router to just change the URL and swap the component instantly.

```jsx
export default function Header() {
    return (
        <header>
            <nav>
                <Link to="/">Home</Link>
                <Link to="/about">About</Link>
            </nav>
        <header>
    )
}
```

## NavLink
* It can `highlight` the current selected link. It has style prop and className prop, which can take a function as the value.
* The React route will pass the function an `obj`. We can destructure it with {isActive}. 
```jsx
<NavLink 
    to="/about"
    className={({isActive}) => isActive ? "my-link" : null }
>
``` 


## useParams()
React router will look at any sections of the path that has a colon before it, and it will add that as the `key` in the key value pair in the object that we get from the useParams().
```jsx
<Route 
    path="/product/:id/:color" 
    element={<ProductDetails />}>
```
```jsx
import { useParams } from "react-router-dom"

export default function VanDetail() {
    const params = useParams()
    console.log(params)
}

>>> {id: 1, color: red}
```

## Nested Route
* We can create a Layout for the parent Route. It will always show.
* Layout doesn't need a path.
* Iy has a `Outlet component`. The Outlet will render the children routes(component) whose `path` matches the `current URL`. 
* The React route can `match multiple routes`. It parent route is always matched if the child route is matched 
```jsx
<Route element={<LearningLayout />}>
    <Route path="/learn/:grade/:semester/:unit/text" element={<Text />} />
    <Route path="/learn/:grade/:semester/:unit/vocabulary" element={<Vocabulary />} />  
</Route>
```
```jsx
export default function LearningLayout() {
    return (
        <>  
            <UnitSelector />
            <ModeSelector />
            <Outlet />
        </>
    )
}
```

## Relative route
* For the child route, start it `without the slash` will make it a relative route. It is relative to the parent route. 
* If the child route's URL is exactly the same as the parent URL, we can still `index` for the path.
```jsx
<Route path="host" element={<HostLayout />}>
    <Route index element={<Dashboard />} />
    <Route path="income" element={<Income />} />
    <Route path="reviews" element={<Reviews />} />
</Route>
```

## end
* If a more nested route matches, it will not match this route!
* It is commonly used to `stop highlight the route` whose URL is same as the parent route if another child route is active. 
```jsx
const activeStyles = {
        fontWeight: "bold",
        textDecoration: "underline",
        color: "#161616"
    }

    return (
        <>
            <nav className="host-nav">
                <NavLink
                    to="/host"
                    end
                    style={({ isActive }) => isActive ? activeStyles : null}
                >
                    Dashboard
                </NavLink>

                <NavLink
                    to="/host/income"
                    style={({ isActive }) => isActive ? activeStyles : null}
                >
                    Income
                </NavLink>

                <NavLink
                    to="/host/reviews"
                    style={({ isActive }) => isActive ? activeStyles : null}
                >
                    Reviews
                </NavLink>

            </nav>
            <Outlet />
        </>
    )
```