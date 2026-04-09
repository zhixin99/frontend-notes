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
            </Routes>
        </BrowserRouter>
    )
}
createRoot(document.getElementById("root")).render(
    <App />
)
```

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