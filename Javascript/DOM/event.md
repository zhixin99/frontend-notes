# Event 
* We will get PointerEvent object in the dev tool.  
* As we scroll down, we will find the target key, which is an object itself.  
* As we extend the target, we will find the following attributes.  
```js
document.addEventListener("click", function(e){
    console.log(e)
})
```

## e.target & event.currentTarget
| Feature                     | `event.target`                                | `event.currentTarget`                                  |
| --------------------------- | --------------------------------------------- | ------------------------------------------------------ |
| What it represents          | The element that actually triggered the event | The element that the event listener is attached to     |
| Usually equals to           | The deepest clicked element                   | The element handling the event                         |
| Safe to use for `FormData`? | ❌ Not always                                  | ✅ Yes (if listener is on `<form>`)                     |
| Typical use case            | Detect what was clicked                       | Access the container or form                           |


## e.target.id - check which id is triggering the event
```html
<div id="container">
    <button>A</button>
    <button>B</button>
    <button>C</button>
</div>
```

```js
let container = document.getElementById("container")

container.addEventListener("click", function(e){
    console.log(e.target.id)
})
```

## e.target.dataset - data attribute
```html
<img src="/images.adb.png" id="img"> 

<!--                        data-[the name i give] = [stored value] -->
<i class="fa-class fa-share" data-share="img"></i>
```

```js
document.addEventListener('click', function(e) {
    // only when you click on the share icon, the e.target.dataset.share will exist
    if (e.target.dataset.share){
        //                   dataset, not data 
        console.log(e.target.dataset.share)
    }
})
```
### JS will flattern out the camelCase in HTML
**Best practice: Use `dash` to seperate words in HTML, and use `camelCase` in the Javascript!**
```html
<i class="fa-class fa-share" data-share-btn="img"></i>
```

```js
document.addEventListener('click', function(e) {
    //                        B here is camel case
    if (e.target.dataset.shareBtn){
        console.log(e.target.dataset.shareBtn)
    }
})
```
`Don't use uppercase` when naming data attributes in HTML
```html
<!--                             shareBtn is camelCase, which will be flatterned out -->
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

## e.target.closest(".classname")
search from the **element that cause the event** and to its parent and grandparent and ... elements, until find the element whose class is the one we need
```js
const form = e.target.closest(".dictation-form")
```

## Event name
### Button
Hover over the button -> mouseenter
```js
declineBtn.addEventListener('mouseenter', function(){
    
})
```