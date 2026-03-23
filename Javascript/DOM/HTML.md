# Basic

`DOM manipulation comes with a cost!`

## Take control of the HTML element
### 1. Built-in shortcut properties
```js
document.body
document.head
document.title
```

### 2. getElementById()
```jsx
document.getElementById
```

### 3.getElementsByClassName()
* It grabs all the element with a given class, and returns a array.
* For each element of the array, we can directly take control of it. 
```js
clearBtn.addEventListener('click', function(){
    const productsArray = document.getElementsByClassName('product')
    for (let product of productsArray){
        product.classList.remove('purchased')
        product.classList.add('on-offer')
        
    }
})
```

### 4. .querySelector()
### Psuodo selector
```js
submitBtn.addEventListener('click', function(){
    const checkedRadio = document.querySelector('input[type="radio"]:checked')
    console.log(checkedRadio.value)
})
```
### Class selector
```js
const box = document.querySelector(".box");
```
### id selector
```js
const header = document.querySelector("#header");
```
### Label selector
```js
// it will select the first p element
const firstParagraph = document.querySelector("p");
```

## Know which HTML element is triggered
### 1. e.target.id
* It always returns a `string`, so when we filter, remember to add a `Number()`!
```js
document.getElementById("click", (e) => {
    console.log(e.target.id)
})
```
### 2. e.target.dataset (data attribute)
```html
<img src="/images.adb.png" id="img"> 

<!-- data-[the name i give] = [stored value] -->
<i class="fa-class fa-share" data-share="img"></i>
```

```js
document.addEventListener('click', function(e) {
    // only when you click on the share icon, the e.target.dataset.share will exist
    if (e.target.dataset.share){
        console.log(e.target.dataset.share)
    }
})
```
* JS will flattern out the camelCase in HTML
* **Best practice: Use `dash` to seperate words in HTML, and use `camelCase` in the Javascript!**
```html
<i class="fa-class fa-share" data-share-btn="img"></i>
```

```js
document.addEventListener('click', function(e) {
    //  B here is camel case
    if (e.target.dataset.shareBtn){
        console.log(e.target.dataset.shareBtn)
    }
})
```
`Don't use uppercase` when naming data attributes in HTML
```html
<!--  shareBtn is camelCase, which will be flatterned out -->
<i class="fa-class fa-share" data-shareBtn="img"></i>
```

```js
// This will never work
document.addEventListener('click', function(e) {
    //                        B here is camelCase
    if (e.target.dataset.shareBtn){
        console.log(e.target.dataset.shareBtn)
    }
})
```
```js
// This will work
document.addEventListener('click', function(e) {
    //                   use b here
    if (e.target.dataset.sharebtn){
        console.log(e.target.dataset.sharebtn)
    }
})
```
### 3. e.currentTarget
* We can also pass in the **e.currentTarget** instead of the form element
```js
const loginForm = document.getElementById('login-form')

loginForm.addEventListener('submit', function(e){
    e.preventDefault()

    const loginFormData = new FormData(e.currentTarget)
})
```

## Write the HTML text
* textContent
```js
// grab a hold of the box-btn and store it in a variable called boxBtn
let boxBtn = document.getElementById("box-btn");
boxBtn.textContent = "Open the box";
```
* innerText
```js
let boxBtn = document.getElementById("box-btn");
// innerText will automatically remove the space between output elements
boxBtn.innerText = "Open the box";
```

## Write the HTML element
```js
let array = ["aa", "bb", "cc"]
const ulEl = document.getElementById("ul-el");
let lineItems = "";

for (let i = 0; i < array.length; i++) {
    lineItems += "<li>" + array[i] + "</li>"
}

// Run the DOM out of the loop to reduce the cost
ulEl.innerHTML = lineItems;
```
* When writing HTML with Javascript, **attribute values** must be `quoted`
```js
src = "xxx"
container.innerHTML = `<img src="${src}">`
```

## Input element & avoid innerHTML
* Without the innerHTML, we will need to use createElement and appendChild to do the same thing
* It doesn't allow malicious JavaScript to be executed.

```js
const h1 = document.createElement("h1")
h1.textContent = "This is imperative coding"
h1.className = "header"

document.getElementById("root").appendChild(h1)
```

## Listen to the event
```js
let boxBtn = document.getElementById("box-btn");

boxBtn.addEventListener("click", function() {
    console.log("I want to open the box")
})
```

## Image src Property
Change the image src in javascript
```js
document.getElementById("myImg").src = "hackanm.gif";
```

## children property
* element.children returns a live HTMLCollection （`array`）which contains all of the child elements of the element upon which it was called.
* If the element has no element children, then children is an empty list with a length of 0.

```html
<div id="cards">
    <div class="card-slot"></div>
    <div class="card-slot"></div>
</div>
```
```jsx
const myElement = document.getElementById("cards");
for (const child of myElement.children) {
    ...
}
```

## .parentElement
* It lets us directly take control of the parent element in js
* It is super useful for the form, because we only get the **id** of the input, but we can take control of the full **form container**.
```js
const container = document.getElementById('container')

container.innerHTML =  `
    <div>
        <input type="radio" id="apple" value="apple">
        <label for="apple">
    </div>
    <div>
        <input type="radio" id="apple" value="apple">
        <label for="apple">
    </div>
    `            
container.addEventListener('click', function(e){
    document.getElementById(e.target.id).parentElement.style.backgroundColor = 'lightblue'
})
```








## .disabled
```html
<!-- set the decrement button as disabled by default -->
<button id="decrement" class="decrement" disabled>-</button>
```
```css
.decrement:disabled{
    color: whitesmoke;
    opacity: 0.2;
    cursor: not-allowed;
}
```

```js
decrement.addEventListener('click', function(){
    quantity--
    if (quantity === 0){
        decrement.disabled = true
    }     
    quantityDisplay.innerText = quantity
})
```