# CSS

## element.style.property - to change the css
```css
.answer{
    display: none;
}

.question{
    background-color: white;
}
```
```js
const answer = document.getElementById('answer')
const revealBtn = document.getElementById('reveal-btn')
const question = document.getElementById('question')

revealBtn.addEventListener('click', function(){
//  element.style.property
    answer.style.display = 'block'
//  change the dash property to camel case
    question.style.backgroundColor = '#68e1fd'

    document.body.style.backgroundImage = `url("https://images.unsplash.com/photo-1471879832106")`
})
```

## classList
### .toggle()
To remove / add the class
```html
<div class="container reverse" id="container">
    <div class="palette-section blue-1"></div>
    <div class="palette-section blue-2"></div>
    <div class="palette-section blue-3"></div>
    <div class="palette-section blue-4"></div>
    <div class="palette-section blue-5"></div>
</div>
<button id="sort-btn">Sort by shade</button>
```

```css
.container {
    display: flex;
}

.reverse {
    flex-direction: row-reverse;
}
```

```js
const sortBtn = document.getElementById("sort-btn")
const container = document.getElementById("container")

sortBtn.addEventListener("click", function(){
    // the class that we want to toggle on and off
    container.classList.toggle("reverse")
})
```

### .add() and .remove()
```css
.unread {
    background: blue;
}

.read {
    background: green;
}
```
```js
document.addEventListener('click', function(e){
    document.getElementById(e.target.id).parentElement.classList.remove('unread')
    document.getElementById(e.target.id).parentElement.classList.add('read')
})
```

