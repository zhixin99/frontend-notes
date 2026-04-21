## e.target & event.currentTarget
| Feature                     | `event.target`                                | `event.currentTarget`                                  |
| --------------------------- | --------------------------------------------- | ------------------------------------------------------ |
| What it represents          | The element that actually triggered the event | The element that the event listener is attached to     |
| Usually equals to           | The deepest clicked element                   | The element handling the event                         |
| Safe to use for `FormData`? | ❌ Not always                                  | ✅ Yes (if listener is on `<form>`)                     |
| Typical use case            | Detect what was clicked                       | Access the container or form                           |


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

## e.stopPropagation()
```js
<div id="parent">
  <button id="child">点我</button>
</div>
```
If we click the button, the event bubbling is like: button -> 
div -> body → document. 
