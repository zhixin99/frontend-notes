# Grid
Margin no longer collapse.  
The default layout of grid is just a single column that lay out all the element vertically.

```CSS
.grid-container {
    display: grid;

    /* Add more columns by declare their width */
    /* grid-template-columns: 1fr 1fr;
    grid-template-rows: 5em 5em; */
    grid-template: 5em 5em / 1fr 1fr;

    /* row-gap: 0.6em; 
    column-gap: 0.3em;  */
    gap: .3em .6em;

    border: 2px solid black;
}
```

## fr
```css
.container {
    /* we have a total of 5 fractions and the first item takes up 2  */
    grid-template-columns: 2fr repeat(3, 1fr);  /* repeat(how many times, what to repeat) */
}
```

```css
.container {
    /* the first item only takes up the space it needs based on the text width  */
    grid-template-columns: auto repeat(3, 1fr);
}
```

## Box alignment
```css
justify-content
align-items
align-self
```

## Placement
### grid-row/grid-column, and span
```css
.grid-container {
    display: grid;
    grid-template: 1fr 3fr 1fr / 1fr 2fr;
}
 
header {
    background-color: palegoldenrod;
    grid-column: span 2;
}
nav {
    background-color: lightcoral;
}
main {
    background-color: lightgreen;
}
footer {
    background-color: gold;
    grid-column: span 2;
}
```

### grid row/grid column, and line numbers
```css
header {
    background-color: palegoldenrod;
    /* grid-column-start: 1;
    grid-column-end: 13; */
    grid-column: 1 / -1;
}
```


### grid-template-areas, grid-area
```css
.grid-container {
    display: grid;
    grid-template: repeat(5, 1fr) / repeat(13, 1fr);
    grid-template-areas: 
        ". nav nav head head head head head head head head head head"
        "nav nav main main main main main main main aside aside aside"
        "nav nav main main main main main main main aside aside aside"
        "nav nav main main main main main main main aside aside aside"
        /* white space: any length of . as long as there's no space between them  */
        ".... .... foot foot foot foot foot foot foot foot foot foot";
}

    
header {
    grid-area: head;
    background-color: palegoldenrod;
}

nav {
    grid-area: nav;
    background-color: lightcoral;
}

main {
    grid-area: main;
    background-color: lightgreen;
}

aside {
    grid-area: aside;
    background-color: lightgray;
}

footer {
    grid-area: foot;
    background-color: gold;
}
```

#### grid-area
```css
.dice {
	display: grid; 
	grid-template: repeat(3, 1fr) / repeat(3, 1fr);
    place-items: center;
}

.pos-1 {
    /* row, column */
	grid-area: 1 / 1
}

.pos-2 {
	grid-area: 1 / 2
}

...

.pos-8 {
    grid-area: 3 / 2
}

.pos-9 {
    grid-area: 3 / 3
}
```
![alt text](../Images/dice-with-pip.png)

## grid-auto-flow: dense & auto-fit
grid-auto-flow: dense - Pack the grid items as dense as possible.  

```css
.grid-container {
    display: grid;
    grid-gap: .5em;
    /* auto-fit: the image will always fuid when needed, and automatically generates as many columns as possible. */
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));

    /* grid-auto-row: specify a given value to all the implicitely generated row tracks.   */
    grid-auto-rows: 75px;

    /* grid will ignore the html order, and remove the extra space */
    grid-auto-flow: dense;
}

.wide {
    grid-column: span 2;
}

.tall {
    grid-row: span 2;
}

.big {
     grid-row: span 2;
     grid-column: span 2;
}
```