# Form

## Elements
| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<label>`       | Label for a form element.                                     |
| `<button>`      | Clickable button.                                             | type
| `<input>`       | Input field (text box, checkbox, etc.).                       | type name placeholder aria-label value  id accept="image/png, image/jpg"
| `<select>` and `<option>` and `<optgroup>`      | Dropdown buttons.                       | value selected size multiple
| `<textarea>`   | Long inputs.                   | 

## Common validation attributes
| Attributes        | Meaning / Use                                                 |    input type | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| required       |                               |
| minlength      |   minlength="8"                                   |  text
| maxlength      |                       |  text
| max      |                       |  number
| min      |    min="21"                   |  number
|pattern| pattern="[a-zA-Z0-9]+" <br>pattern="[a-zA-Z]{3}"
|defaultValue|  set a default value to the input so that the user don't need to type everytime <br> defaultValue="Jean"| 


## Accessibility
always add a label and placeholder for the input form
```html
<!--   associate a label to the element id  -->
<label for="city">City</label>

<!-- name is to reference form data after a form is submitted. -->
<input 
    type="text" 
    name="city"
    id="city"
    placeholder="London"
>
```
If there's no label, we should give it an aria-label
```html
<input 
    type="text"
    name="ingredient"
    placeholder="e.g. oregano"
    aria-label="Add ingredient"
/>
```

## e.preventDefault() 
To prevent getting a query string in the URL and refresh the page. 
```js
document.getElementById("form").addEventListener("submit", function(e){
    e.preventDefault()
})
```



## Get the input value
### 1. FormData function
* It takes in the **form element** as the parameter.   
* Put the `name` of the input element to get the value. 
* It will return an **object** holding all the data, `key` is the `input name`, `value` is the input `value`. 

```js
const loginForm = document.getElementById('login-form')

loginForm.addEventListener('submit', function(e){
    e.preventDefault()

    const loginFormData = new FormData(loginForm)
    console.log(loginFormData)
    >>> FormData {}

    // Use FormData.get(key) to get the value
    // Put the name of the input element as the key
    const name = loginFormData.get("astronautName")
    const email = loginFormData.get('astronautEmail')
})
```  


### 2. .value
* It is taking the `id`.
* The value is always in the format of `string`!
```js
const input = document.getElementById("input");
               // value property
console.log(input.value);
```
* Clear input value
```js
const input = document.getElementById("input");
    // value property
input.value = "";
```
It is **not allowed** to use `form.value` because form is just a **container**. Only `input` has value as the property! 

## Reset the form
```js
function handleSubmit(event) {
    event.preventDefault()
    const formEl = event.currentTarget
    const formData = new FormData(formEl)
    const email = formData.get("email")
    formEl.reset()
  }
```

## Clear the form 
It will clear all the input areas in the form
```js
const form = document.getElementById("new-post")
form.reset()
```

## Submit button
2 ways of making the submit button:   
- a special input type   
```html
<form>
    <input type="submit">
</form>
```
- use a regular HTML button 
```html
<form>
    <!-- any button that is inside of the form tag is taken as the submit button -->
     <!-- type="submit" is not neccessary, but it is good for clarity -->
    <button type="submit">submit</button>
</form>
```
### Add event listener for form submission
* Use `form` as the element, not the submit button
* Event name is "submit"
```js
const form = document.getElementById("form")

form.addEventListener("submit", function(){
    ...
})
```

## Reset button 
```html
<form>
    <button type="reset">
        Reset
    </button>
</form>
```

## Decline button
```html
<form>
    <button type="button">
        Decline
    </button>
</form>
```

## Checkbox
```html
<div>
    <label for="accept-terms">
        I accept these terms and conditions
    </label>
    <input type="checkbox" id="accept-terms">
</div>
```
- Use `<fieldset>` and `<legend>` tags to group the set and provide the context for screen reader users
- Give each input element a `name` and a `value` so we can get from formData.
```html
<fieldset>
    <legend>Dietary restrictions:</legend>
    <label>
        <input type="checkbox" name="dietaryRestrictions" value="kosher" />
        Kosher
    </label>

    <label>
        <input type="checkbox" name="dietaryRestrictions" checked value="full-time" id="checkbox-gluten"/>
        Gluten-free
    </label>
</fieldset>

```
Eventlistener is `change`
```js

checkboxGluten.addEventListener('change', function(){
    if (acceptTerms.checked){...}
})
```
### toggle switch
```html
<!-- Rectangular switch -->
<label class="switch">
  <input type="checkbox">
  <span class="slider"></span>
</label>

<!-- Rounded switch -->
<label class="switch">
  <input type="checkbox">
  <span class="slider round"></span>
</label>
```

## Radio buttons
- Use `<fieldset>` and `<legend>` tags to group the set and provide the context for screen reader users
- We must assign a `value` to the option of each radio, and that is the value that we are going to get from the formData. 
- Giving the radios the same `name` can create a radio group in which only one choice can be selected. 
- `defaultChecked` is a property for the radio buttons
```html
<fieldset class="radio-container">
    <legend>Do you have cats?</legend>
    <label for="yes">Yes</label>
    <input 
        type="radio" 
        name="cats"
        value="name"
        defaultChecked="true"
        class="contact-radio"
        id="yes">

    <label for="no">No</label>
    <input 
        type="radio" 
        name="cats"
        value="no"
        class="contact-radio"
        id="no">
</fieldset>
```
* To get the id of the input that is clicked. 
```js
const yesBtn = document.getElementById("yes")
// for checked radio, the event is `change`
yesBtn.addEventListen("change", function(e){
    console.log(e.target.id)
})
```
* To get the value of the `checked` radio. 
```html
<form id="form">
    <input type="radio" name="emotion" value="happy">
    <input type="radio" name="emotion" value="sad">
</form>
```
```js
const form = document.getElementById("form")
new FormData(form).get("emotion")

>>> happy
```
or we can use querySelector
```js
document.querySelector('input[name="emotion"]:checked').value
```

## Dropdown button
- Give the select element a `name` and give each option a `value`.  
- `defaultValue` property will show the given value as the default value.  
- `size` represents how many items shown in the scroll bar without scroll.   
- We can put a `value of empty string` and put some instruction texts as the 1st option, make it `disabled`, and make the **select** element `required`.
- Group options together in the `optgroup` if needed.

```html
<section class="container">
    <form>
        <label for="superpowers">Choose Your Superpower:</label>
        <select id="superpowers" size="6" name="superpowers" defaultValue="indigo" required>
            <option value="" disabled>-- Choose a color --</option>
            <optgroup label="physical">
                <option value="flight">Flight</option>
                <option value="invisibility">Invisibility</option>
                <option value="superStrength" selected>Super Strength</option>
            </optgroup>
            <optgroup label="psychological">
                <option value="telepathy">Telepathy</option>
                <option value="timeTravel">Time Travel</option>
                <option value="wisdom">Wisdom</option>
            </optgroup>
        </select>

        <button type="submit">Reveal My Superpower</button>
    </form>
</section>
```
We can get the value of the currently selected dropdown option
```js
const superPowers = document.getElementById("superpowers")

superPowers.addEventListener("change", () => {
    console.log(superPowers.value)
})
```

## Textarea
```html
<div class="container">
    <textarea 
        placeholder="Ask me anything!" 
        id="chat-input"
    ></textarea>        <!-- need to keep the opening tag and closing tag together in one line -->
    <button id="talk-btn">Talk to me!</button>
</div>
```

```css
textarea{
    /* can't resize the text area */
    resize: none;
}
```
We can get the textarea value, same as the input element. 
```js
const talkBtn = document.getElementById('talk-btn')
const chatInput = document.getElementById('chat-input')

talkBtn.addEventListener('click', function(){
    console.log(chatInput.value)
})

```

## Slider
```html
<div>
  <input type="range" id="volume" name="volume" min="0" max="11" />
  <label for="volume">Volume</label>
</div>
```
```css
/* change the slider thumb */
.password-length {
    accent-color: #8B5CF6;
    cursor: pointer;
    vertical-align: middle;
}
```
```js
range.addEventListener("input", function(){
    lengthValue.textContent = range.value
})

```




