## Handle functions
https://react.dev/reference/react-dom/components/common
### MouseEvent handler function 
```JSX
<div
    onClick={e => console.log('onClick')}
    onMouseEnter={e => console.log('onMouseEnter')}
    onMouseOver={e => console.log('onMouseOver')}
    onMouseDown={e => console.log('onMouseDown')}
    onMouseUp={e => console.log('onMouseUp')}
    onMouseLeave={e => console.log('onMouseLeave')}
/>
```

## Form 
onchange and onSubmit
```jsx
import { useState } from 'react';
import { createRoot } from 'react-dom/client';

function MyForm() {
  const [name, setName] = useState("");

  function handleChange(e) {
    setName(e.target.value);
  }

  function handleSubmit(e) {
    e.preventDefault();
    alert(name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>Enter your name:
        <input
          type="text" 
          value={name}
          onChange={handleChange}
        />
      </label>
      <input type="submit" />
    </form>
  )
}

createRoot(document.getElementById('root')).render(
  <MyForm />
);
```

## Add eventListener
```jsx
function App() {
    return (
        <main className="container">
        <img
            src="https://picsum.photos/640/360"
            alt="Placeholder image from Picsum"
        />
        <button onClick={function() {console.log("Clicked!")}}>Click me</button>
        </main>
    )
}
```
Or we can put the function ahead of the html parts:  
- **No parenthesis** otherwise the function will run immediately 
- We should pass the contents of the function or the functionality to the button
```jsx
function App() {

    function handleClick() {
        console.log("I was clicked!")
    }
    
    return (
        <main className="container">
        <img
            src="https://picsum.photos/640/360"
            alt="Placeholder image from Picsum"
        />
        <button onClick={handClick}>Click me</button>
        </main>
    )
}
```

## value
Update the state property when the user input something as the topText
```jsx
import { useState } from "react"

export default function Main() {
    const [meme, setMeme] = useState(
        {
            topText: "One does not simply",
            bottomText: "Walk into Mordor",
            imageUrl: "http://i.imgflip.com/1bij.jpg"
        }
    )

    function handleEvent(e){

        const {value} = e.currentTarget

        setMeme(prevMeme => {
            return (
                {...meme, topText: value}
            )
        })
    }

    return (
        <main>
            <input 
                type="text"
                onChange={handleEvent}
            />
        </main>
    )

}

```

