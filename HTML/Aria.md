# ARIA
* ARIA shorts for Accessible Rich Internet Applications. 
* It fills in a gap when HTML's native sementics fall short. 

## aria-checked
Indicates whether the element is checked (true), unchecked (false)
```html
<div 
    id="toggleTheme" 
    onclick="toggleTheme()" 
    role="switch" 
    aria-checked="false" 
    tabindex="0"
>
    Light Mode
</div>
```

## aria-label
direct the assistive technology how it should describe how the button is supposed to do
```html
<button id="get-activity" aria-label="Find a new activity."></button>
```

## aria-press
for the buttons, to indicate if they are pressed
```jsx
return (
    <button 
        style={styles}
        onClick={props.hold}
        aria-pressed={props.isHeld}
        aria-label={`Die with value ${props.value}, 
        ${props.isHeld ? "held" : "not held"}`}
    >{props.value}</button>
)

```

## aria-live
tell the assistive technology when a DOM change happens to this element, it should read out the new value of the content
```html
<p id="activity" aria-live="polite">Find something to do</p>
```
### An example to show win status
```jsx
return (
    <div aria-live="polite" className="sr-only">
        {gameWon && <p>Congratulations! You won! Press "New Game" to start again.</p>}
    </div>
)
```
```css
.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
}
```