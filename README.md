# HTML & CSS Carousel

This example is a lightweight implementation of a Slide Carousel, using HTML and CSS only, Why is this important? Carousels are one of the most popular ways of showing self-contained information, there are several implementations such as [jCarousel](http://sorgalla.com/jcarousel/) or [Bootstrap's Carousel](https://getbootstrap.com/examples/carousel/), but sometimes loading a complete library for adding a simple feature like this may be an overkill.

Here is the basic structure of a carousel, although the `<ul>` tag is normally used to list text I will use it for structure purposes only, which means that the `<li>` elements will be containers for anchors, images or anything we need to display.
``` html
<div id="carousel">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>1</li> <!-- repeated element -->
        </ul>
</div>
```

Then we need to style our carousel container, we use the id selector since we normally need a single carousel per document, otherwise is prefereble to use the class selector, in this rule I center the element horizontally (`margin:auto;`) and give a fixed dimension to it (200px high and 200px wide). The `overflow:hidden;` rule is used to display partially our list of elements with the intention of showing a single slide. Finally the `position:relative;` rule is used to add a reference point to our `<ul>` element which will use absolute positioning.

``` css
#carousel
{
    height:200px;
    width:200px;
    overflow: hidden;
    position:relative;
    margin:auto;
}
```

Now for the `<ul>` element we will remove bullets using `list-style-type:none;` and we'll make use of flexbox (`display:flex;`), which makes extremely easy to align elements horizontally (`flex-direction:row;`), we also remove margin and padding and set position to absoulte, this will allow us to use the left property to move our elements. 

``` css
#carousel ul
{
    list-style-type: none;
    display:flex;
    flex-direction: row;
    padding:0px;
    margin:0px;
    position: absolute; 
    animation: slide 25s cubic-bezier(0.05, 0.9, 0, 1) infinite;
}
```

Finally we set the animation called slide to this element, and here is where the magic happens. The slide animation will move our elements list with a step of 200px, which is the elements width. Our first position will be `left:0px;` and because we are using absolute position refered to the container (Yes, I know absolute means free of references...) it will start showing our first element, in the next interval we will move our list 200px left, showing our second element, the process continues up to our fifth element wich is shown with `left:-800px; ` at this point our work is done (Leonard Nimoy disappearing in the background) and to restart our animation without moving abruptly to the start we inserted a sixth element, which is a copy of our first element and is shown with `left:-1000px`, then we move instantly to our first position and repeat the process (this is done with `animation-direction:normal;` but we omit it since it is the default value). A cubic-bezier timing function is used to ease the transition and we set a 25 seconds period to the entire animation. 

```css
@keyframes slide{
    0%{left:0px;}
    20%{left:-200px;}
    40%{left:-400px;}
    60%{left:-600px}
    80%{left:-800px}
    100%{left:-1000px}
}
```
Finally we add simple style to our `<li>` elements although this depends on the content you want to show. `display:flex`, `align-items:center` and `justify-content:center` is used to center our text both horizontally and vertically.

```css
#carousel li
{
    display:flex;
    align-items: center;
    justify-content:center;
    width:200px;
    height: 200px;
}

li:nth-child(1),li:nth-child(6){
    background-color: #ff66ff;
}
li:nth-child(2){
    background-color: #66ff66;
}
li:nth-child(3){
    background-color: #3399ff;
}
li:nth-child(4){
    background-color: #ff9966;
}
li:nth-child(5){
    background-color: #ff3300;
}
```

A link to our Carousel example running on github pages: [HTML & CSS Carousel](https://alejandromdz.github.io/html_css_carroussel)
