# Accessibility
* Color contrast => 4.5: 1
* Pair the color with shape
* Alt text for img

## aria-label
* Add it for input, Link, button, to give the screen reader for context.
* In this case, if we don't add the aria-label, the screen reader will just say A, B, C; But with the aria-label, the user know it is actually a letter. 
```jsx
<button
    aria-label={`Letter ${letter}`}
>
    {letter.toUpperCase()}
</button>
```

## aria-live & role
* Check if any part of the page is dynamically rendered, including the popup, search result...
    * polite: If the user is currently reading a paragraph, the screen reader will not interrupt them. It waits until the user stops typing or the screen reader finishes speaking its current sentence.
    * assertive: Interrupts immediately. Clears the screen reader's queue and drops everything to read the update.
```jsx
<section 
    aria-live="polite" 
    role="status"
    className={gameStatusClass}
>
    {renderGameStatus()}
</section>
```

## sr-only section
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

## aria-disabled
* Announce when a `button is disabled`
* In this case, when the users uses a tab key to tab through all the letters, so we disable the ones which have already been chosen.
```jsx
const keyboardElements = alphabet.split("").map(letter => {
    const isGuessed = guessedLetters.includes(letter)
    const isCorrect = isGuessed && currentWord.includes(letter)
    const isWrong = isGuessed && !currentWord.includes(letter)
    const className = clsx({
        correct: isCorrect,
        wrong: isWrong
    })

    return (
        <button
            className={className}
            key={letter}
            disabled={isGameOver}
            aria-disabled={guessedLetters.includes(letter)}
            onClick={() => addGuessedLetter(letter)}
        >
            {letter.toUpperCase()}
        </button>
    )
})
```

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





* aria: aria-live, aria-press, aria-checked, aria-label
