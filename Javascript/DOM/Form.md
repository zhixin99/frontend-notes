# Form


## e.preventDefault() 
To prevent getting a query string in the URL and refresh the page. 
```js
document.getElementById("form").addEventListener("submit", function(e){
    e.preventDefault()
})
```

## FormData function (a constructor function)
It will return an **object** holding all the forms data.    
It takes in the **HTML form element** as the parameter.   
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
```html
<form id="login-form">
    <label for="astronautName">Astronaut Name 👩‍🚀</label>
    <input 
        type="text" 
        id="astronautName" 
        name="astronautName"  
        placeholder="Neil Armstrong"
        required
        >
    <label for="astronautEmail">Astronaut Email</label>
    <input 
        type="email" 
        id="astronautEmail" 
        name="astronautEmail" 
        placeholder="n.armstrong@nasa.com"
        required
        >
    <button type="submit">submit</button>
</form>    
```
We can also pass in the **event.currentTarget** instead of the HTML form element
```js
const loginForm = document.getElementById('login-form')

loginForm.addEventListener('submit', function(e){
    e.preventDefault()

    const loginFormData = new FormData(e.currentTarget)
})
```

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

## Get input value
The value is always in the format of `string`!
```js
const input = document.getElementById("input");
               // value property
console.log(input.value);
```

## Clear input value
```js
const input = document.getElementById("input");
    // value property
input.value = "";
```

## Clear the form 
It will clear all the input areas in the form
```js
const form = document.getElementById("new-post")
form.reset()
```





