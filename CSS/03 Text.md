# Text
## italic
```css
font-style: italic;
```
## underline
```css
a {
	text-decoration:underline dotted;
}
```

## text-transform
```css
.headline {
     text-transform: uppercase;  /* lowercase, capitalize */
}
```

## font-size
### the rem unit - root em
We use `rem` for font-size to avoid the `compounding issue`.
1rem = 16px
```css
p {
      font-size: 1rem;
}
```
Only if we change the html font-size, 1rem will change  
```css
html {
    font-size: 20px;
}
```
### the em unit
A font-size value set in em is relative to the font size of the parent element.
If there's no font-size set for all the parents' elements, it will take `16px` as the default 1em.  

It is not commonly used because of the compounding issues.

## default margin
h1 has the default margin
```css
main h1 {
    margin: 0;
}
```

## font-family & @font-face
* download the font and drag the ttf file in the folder
```css
@font-face {
    src: url("xxx.ttf");
    /* name for the local font */
    font-family: Corleone;
}

h1 {
    font-family: Corleone;
}
```

## line-height
In CSS, if you want the line-height to be exactly the same as the text height, you should set the line-height value to **1**.
```css
.text-element {
    /* Method 1: Unitless (Recommended) */
    line-height: 1;

    /* Method 2: Percentage */
    line-height: 100%;

    /* Method 3: Same as font-size */
    font-size: 16px;
    line-height: 16px;
}
```
![alt text](../Images/line-height.png)

## Links and buttons
- links are for navigation, go to another location.  
- Buttons are for interaction. (Open a model)  
You can style the link like a button.