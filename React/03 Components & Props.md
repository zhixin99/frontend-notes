## Component
React components are meant to be `pure functions`.
* When it is given same props or state, should always return the same interface. 
* Rendering and re-rendering a component will never have any kind of side effect on an outside system

# Props
We can pass neccessary props to the component when creating a new instance of the component
```jsx 
// Contact.jsx
export default function Contact(props) {
    console.log(props)
    return (
        <article className="contact-card">
            <h3>{props.name}</h3>
        </article>
    )
}
```
```jsx 
// App.jsx
import Contact from "./Contact"
export default function App(props) {
    return (
        <main>
            <Contact name="Jean" location="Singapore"/>
            <Contact name="David" location="Netherlands"/>
        </main>
    )
}
```
```jsx
// Index.jsx
import { createRoot } from "react-dom/client"
import App from "./App"

createRoot(document.getElementById("root")).render(<App />)

// It will log out objects with all the keys and values that we passed in when calling the component
>>> {name: "Jean", location="Singapore"}
>>> {name: "David", location="Netherlands"}
```

## key
* key helps React identify which items in an array have changed, been added, or removed, so it can update the DOM efficiently.
* key can't be passed to the child component
* When we `map over` an array and create an `array of jsx element`, React needs the key that is dedicated to jsx element, so it can keep track of items every time something got rerendered.
```jsx
// Dice.jsx
export default function Dice(props) {
    return (
        <button>props.value</button>
    )
}
```
```jsx
// App.jsx
export default function App() {
    const array = [1, 2, 3]
    // Here, we create an array of jsx elements, and it need key
    const diceEl = array.map(number => <Dice 
        value={number}
        key={number} 
    />)
    return (
        <main>
            diceEl
        </main>
    )
}
```
### nanoid
A third party package that give us the id automatically
```jsx
import { nanoid } from "nanoid"

const [dice, setDice] = useState(generateAllNewDice())

function generateAllNewDice() {
    return new Array(10)
        .fill(0)
        .map(() => ({
            value: Math.ceil(Math.random() * 6), 
            isHeld: false,
            id: nanoid()
        }))
}
```

## Pass Different Data Types
### Numbers
Numbers has to be sent inside curly brackets to be treated as numbers:
```jsx
createRoot(document.getElementById('root')).render(
    <Car 
        year={1969} 
        comments={[
        {author: "", text: "", title: ""},
        {author: "", text: "", title: ""}
        ]}
        img={{ 
            src: "https://scrimba.com/links/travel-journal-japan-image-url",
            alt: "Mount Fuji" 
        }}
    />
);
```

### JSX element
wrap the JSX element in {}
```jsx
<LearnSection 
    icon={<i class="fa-solid fa-layer-group section-header-icon"></i>}
    title={t('dashboard.courses')}
>
    <div className="all-courses-container">
        {unitsEl}
    </div>
</LearnSection>
```

### Bolean
```jsx
<ProjectCard
    isFeatured={true}
/>

```

### Pass on object to props
```jsx
export default function App() {
    
    const entryElements = data.map((entry) => {
        return (
            <Entry
                key={entry.id}
                entry={entry}
            />
        )
    })
    
    return (
        <>
            <Header />
            <main className="container">
                {entryElements}
            </main>
        </>
    )
}
```
```jsx
export default function Entry(props) {
    return (
        <article className="journal-entry">
            <div className="main-image-container">
                <img 
                    className="main-image"
                    // entry is a property of props, and img is a property of entry
                    src={props.entry.img.src} 
                    alt={props.entry.img.alt}
                />
            </div>
        </article>
    )
}
```

## children property
- In React, whenever you put something inside a component's tags, React passes those elements to the component via a special prop called **children**.
- React evaluates children dynamically depending on what you pass:
    - 0 items: children is undefined.
    - 1 item: children is a single React Element `(object)`.
    - 2+ items: children becomes an `array` of React Elements.
```jsx
export default function ContentSection({sectionHeader, children}) {
    return (
        <div className="project-details-section">
            <h3 className="project-details__content-title">{sectionHeader}</h3>
            {children}
        </div>
    )
}
```
```jsx
import ContentSection from "./ContentSection"

export default function ProjectContent() {
    // all the codes between <ContentSection> and </ContentSection> are passed to the ContentSection as the children property
    return (             
        <ContentSection
            sectionHeader="See Live"
        >
            <a href="#" className="btn" target="_blank">Live Link</a>
            <p>Check out the deployment!</p>
        </ContentSection>
    )
}
```
In this case, children will be an array containing two objects: 
```jsx
[
  { type: "a", props: { ... } },
  { type: "p", props: { children: "Check out the deployment!" } }
]
```

## props spreading
- When you use {...props} inside a JSX tag, you are telling React: "Take every key-value pair inside this object, **unpack** them, and hand them over as individual **attributes** to this HTML element." So the `props key` should be `native HTML attributes`!
```jsx
// App.js
import Button from './Button';

export default function App() {
    return (
        <Button 
            type="submit"
            className="primary-btn" 
            onClick={() => alert('Clicked!')}
        >
            Click Me!
        </Button>
    );
}
```
What Button component receives:
```js
props = {
    type: "submit",
    className: "primary-btn",
    onClick: () => alert('Clicked!'),
    children: "Click Me!"
};
```
When `React` compiles your code, the spread operator unpacks that props object. It strips away the outer curly braces of the object and writes the properties directly into the <button> HTML tag as individual attributes.
```jsx
<button 
    type={props.type} 
    className={props.className} 
    onClick={props.onClick}
    children={props.children} 
>
```

## destructure props
```jsx
export default function Contact({img, name}) {
    return (
        <article className="contact-card">
            <img
                src={img}
                alt="Photo of Mr. Whiskerson"
            />
            <h3>{name}</h3>
        </article>
    )
}
```
```jsx
import Contact from "./Contact"

export default function App() {
    return (
        <div className="contacts">
            <Contact
                img="./images/mr-whiskerson.png"
                name="Mr. Whiskerson"
            />
            <Contact
                img="./images/fluffykins.png"
                name="Fluffykins"
            />
        </div>
    )
}
```

## rest operator
* It is very useful when we need to combine **destructure props** and **props spreading**.
* ...rest is another `object`. 
    - In most cases, it stores all the key-value pairs from props whose key is the `native HTML attributes`, so that we can separate the other properties.
    -  In this case, since children is not HTML attributes, it will be meaningless if we only use props spreading. 
```jsx
export function Button({children, ...rest}) {
    return (
        <button 
            {...rest}
        >
            {children}
        </button>
    )
}
```

## compond components
- Components that **work together** to accomplish a greater objective than might make sense to try and accomplish with a single component alone.
- compound components help you avoid having to **drill props** multiple levels down. Compound component "flatten" the heirarchy. Since I need to provide the children to render, the `parent-most component` has **direct access** to those "grandchild" components, to which it can pass whatever props it needs to pass **directly**.


## Spread object
```jsx
export default function App() {
    
    const entryElements = data.map((entry) => {
        return (
            <Entry
                key={entry.id}
                // equals to 
                // img={entry.img}
                // location={entry.location}
                // ...
                {...entry}
            />
        )
    })
    
    return (
        <>
            <Header />
            <main className="container">
                {entryElements}
            </main>
        </>
    )
}
```