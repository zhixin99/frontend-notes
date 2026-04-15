# Image

## alt text
```html
<img src="husky.png" alt="a cheeky smiling husky">
```

## background
```css
.container {
	/* always put a background color simlar to the image color */
    background: #9480e4 url("images/intro-bg.png");
    background-repeat: no-repeat;
    background-position: right;
    background-size: cover;
}
```
<img src="../Images/blend.png" width="400">

### background-blend-mode
```css
.about-section {
    background-image: url(images/clouds.jpg);
    background-color: rgba(255, 255, 255, 0.5);
    background-blend-mode: lighten;
    background-size: cover;
}
```

### background-size
1. background-size: cover => it will always stretch the image to cover the whole place.   
* In wide screen, the top and bottom can be cropped.   
<img src="../Images/cover-wide.png" width="400">

* In narrow screen, the right and left can be cropped.   
<img src="../Images/cover-narrow.png" width="200">

2. background-size: contain => it will always contain the whole image.   
* In narrow screen, it may look wired if we still use the image for the wide screen.   
<img src="../Images/contain.png" width="200">

3. background-size: auto 100% => it will cut the right and left side if needed, but make sure the top and bottom is not cut. 
<img src="../Images/customized-wide.png" width="400">
<img src="../Images/customized-narrow.png" width="200">

## Resize the image: object-fit
1. We can set the container and set it the correct width and height we want
```html
<div className="main-image-container">
    <img 
        className="main-image"
        src="https://scrimba.com/links/travel-journal-japan-image-url" 
        alt="mount fuji" 
    />
</div>
```
```css
.main-image-container {
    width: 125px;
    height: 168px;
    overflow: hidden;
}
```
2. sets how the content of the image should be resized to fit its container.
```css
img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
```

## role and aria-label when you can't use an HTML img tag
make the `container div and everything inside` treated as an image.  
```html
<!-- the screen reader will skip all the children content inside the container, so the aria-label needs to include the text inside.  -->
<div class="meme-container" role="img" aria-label="A cheeky smiling dog with text saying 'when the cat gets blamed for something you did'.">
    <div class="meme-text">
        <h1>
            When the cat gets blamed for something you did
        </h1>
    </div>
</div>
```
```css
.meme-container {
    background-image: url('husky.jpeg');
    background-size: cover;
}
```

## Float property
```css
img {
    height: 100px;
    border-radius: 10px;
    padding: 0;
    margin: 5px 10px 5px 0;
    /* img with text around it */
    float: right; 
}
```
<img src="../Images/float.png" width="200">

```css
Remove any float
.para-1 {
    /* nothing will float to the right side of the element */
    clear: right;
    clear: both;
}
```
Stretch the container to include the float inside. 
```css
.para-3 {
    display: flow-root;
}
```
<img src="../Images/parent-float.png" width="300">
