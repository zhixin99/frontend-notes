# Postion

## Position: relative and absolute
the absolute element is `above` the other elements
```css
.map-container {
    /* without the relative parent element, the child element will position itself relative to the whole window */
    position: relative;
}

.sun-icon {
    /* the element needs to know where to start measuring */
    position: absolute;
    top: 0;
    left: 0;
}
```
We can also use percentage instead of pixel
```css
buttons {
    position: absolute;
    /* make the button center of the flex, regardless of other elements in the flex box. */
    left: 50%;
    transform: translateX(-50%);
}
```

## Position: fixed
It is always obscuring everything until the user get rid of it.  

It is always relative to the window and it is always there no matter how you scroll.
```css
.pop-up{
    /* put in the center of the browser window */
    position: fixed;
    /* top: 0; bottom: 0; left: 0; right: 0; */
    /* It makes the element stretch to all four edges of the viewport, filling the entire screen. */
    insert: 0; 
    margin: auto;
}
```

## z-index
it controls the z axis order of positioned elements and their descendents  

```css
/* the default stacking context is the html, and the absolute elements can go behind the container.   */

.container {
    position: relative;
    background-color: deeppink;
    z-index: auto /*default*/
}

card {
    position: absolute;
}

.card-1 {
    left: 0; 
    top: 0;
    z-index: 1; /*it will come in front of all the cards*/
}
.card-2 {
    left: 15px; 
    top: 25px;
    z-index: -1; /*it will disappear*/
}
```

```css
/* z-index 0 establishes a stacking context. Elements are not stacking relative to the html. They are stacking relative to their container.   */

.container {
    background-color: deeppink;
    position: relative;
    z-index: 0 
}

card {
    position: absolute;
}

.card-1 {
    left: 0; 
    top: 0;
    z-index: 1; 
}
.card-2 {
    left: 15px; 
    top: 25px;
    /*The card will never stack behind the container*/
    z-index: -1; 
}
```