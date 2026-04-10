## rule
Write your basic CSS with mobile device in mind first.

Use media queries to adjust the design and layout for wider screen users. 

## Size
```css
@media (min-width: 420px) {
}

@media (min-width: 550px) {
}

@media (min-width: 720px) {  
}

@media (min-width: 850px) {  
}
```

## font-size
```css
@media (min-width: 500px) and (max-width: 799px) {
    
    h1 {
        font-size: 3.5rem;
    }
}
```

## padding
The padding in mobile view is usually smaller than the wider screen
```css
header, 
section, 
footer {
    padding: 1.25em 0; 
}


@media (min-width: 768px) {
    header,
    section,
    footer {
        padding: 2.875em 0;        
    }
}
```

## button
```css
.btn {
    display: block;
}

@media (min-width: 768px) {
    .btn {
        display: inline-block;
        margin-right: 0.5rem;

    }
}
```

## navigation bar
```css
/* basic css */
nav a {
    font-size: 1.125rem;
    padding: 0.85em 0;
    display: block;
}

/* for narrow screen */
@media (max-width: 767px) {
    header {
        text-align: center;
    }

    nav {
        margin-top: 1.5em;
    }  

    li:not(:last-child) {
        border-bottom: 1px dotted #a190b6;
    }  
}

/* for wider screen */
@media (min-width: 768px) {
    header .container, 
    ul {
        display: block
    }

    header.container {
        align-items: center;
        justify-content: space-between;
    }

    nav li {
        margin-left: 1.25em;
    }
}

```



