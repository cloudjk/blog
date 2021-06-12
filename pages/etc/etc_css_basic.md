---
title: CSS Basic
sidebar: mydoc_sidebar
permalink: etc_css_basic.html
folder: etc
---

#### 1. Text Transform
transfrom text to upppercase, capitalize ...

```css
span{ 
text-transform: uppercase; 
}
span{
    text-transform: capitalize:  //  How are you => How Are You
}
```    


#### 2. Text Decoration
Remove underline in a Tag, show overline, line-through ...

```css
a{ 
    text-decoration: none; 
}

article{
    text-decoration: overline;
}
a{
    text-decoration: inherit; // inherit text-decoration declaration in article
}
```


#### 3. Conflicts & the Cascade~

1. **If the selectors are identical, bottom most rule always wins.**

```css
p { color: black; }
p { color: red; }  # <- This rule wins
```     

2. **Specific rule wins**

```css
# main-content p{ color: black; }  # <- This rule wins (101 point)
p {color: red; }   (1 point)
```

3. **How Specific ?**
- ID's     : 100 points
- Classes  : 10 points
- Elements : 1 point

**But, bear in mind that this specificity applies only when the style explicilty targets the tag, id or classes.**  
**When it comes to inheritance, point does not count.**  

![Specificity](/assets/img/posts/conflictsAndCascase.png)

In this case, '#main-concept p' style targets only to p tag not strong tag. Strong tag inherits style but 
in inheritance, point does not count. So by putting in strong tag and its style, text displays green color.

#### 4. Inheritance
Styles are inherited to childs.

#### 5. Default brower style
**a tag** does not inherit style. It has its own browser style for each brower.

#### 6. Important declaration
1) Nothing can override to the important declaration. No matter what other rules try to override this !!!  
2) Do not use too often.

```css
p{
    color: red !important;
}
```

#### 7. Targeting Multiple Elements

All p, span, a, li tags apply same style.

```css
p, span, a, li{
    color: red;
    font-size: 14px;
    font-weight: bold;
    font-family: Arial;
}
```

#### 8. Descendant Selectors

```html
<div id="main-content">
    <p> Hello there <strong>ninjas!</strong> contact us below.</p>
    <p> Aren't paragraph's cool?</p>
    <div id="sub-content">
        <p>More content</p>
    </div>
</div>
```

1) all p tags(including in sub-content) which are descendants of main-content id will apply the style.

```css
#main-content p{
    color: red;
}
```

2) If you want to apply different style to sub-content which has p tag, you can do either of them.

```css
#sub-content p{
    color: red;
}

#main-content #sub-content p{
    color: red;
}
```

#### 9. Direct Children Combinator

direct children of main-content id will be applied the style.

```css
#main-content > p{
    color: red;
}
```

#### 10. Adjacent Selectors

Adjacent selector only applies the style to the adjacent selector.

```html
<div id="all-articles">
    <h2><Article #1</h2>
    <p>Published by the Net Ninja</p>
    <p>blah blah blah</p>
    <p>blah blah blah</p>
    <p>blah blah blah</p>
</div>
```
```css
#all-articles h2 + p{
    color: green;
}
```

#### 11. Attribute Selectors

1) Attribute selectors apply the style to all tag attributes associated with it.  
2) Apply the style to all span tag which has class attribute  

```css
span[class]{
    color: purple
}
```

3) Apply the style to all div tag which has id attribute 

```css   
div[id]{
    background: grey;
}
```

4)  Apply the style to all a tag which has title attribute and title name is "search engine"

```css
a[title="search engine"]{
    color: red;
}
```

5) Pattern matching: let the style of class deck to appear anywhere in space deliminated list using "~=" pattern

```css
span[class~="deck"]{
    color: purple;
}    
<span class="deck halls">Yo, I'm a span tag too</span>
<span class="deck">This is a deck of spans</span>
<span class="deck">I like span decks</span>
```

6) Pattern matching: apply the style to all attributes when its value ends with assigned attribute name using "$=" pattern

```css
a[href$="pdf"]{
    color: green;
}
<a href="something.pdf">pdf file</a>
<a href="something2.pdf">pdf file2</a>
```

7) Pattern matching: apply the style to all attributes when its value starts with assigned attribute name using "^=" pattern

```css
a[href^="http"]{
    color: pink;
}
<a href="http://www.google.com" title="Google">I am a Google link</a>
<a href="http://www.github.com" title="Github">I am a Github link</a>
```

#### 12. Pseudo Classes Concept

1) Pseudo Classes are an extension to normal CSS selectors, to target more specific things.

Behavioural Pseudo Classes  
=> Allow us to style an element in relation to user actions, such  as :  
- Whether a link is being hovered over  
- Whether a button is being pressed  
- Whether a tick box has been checked

2) Structural Pseudo Classes => Allow us to style elements based on adavanced structural techniques not possible from ordinary CSS selectors : - The 5th <li> tag in a list - A parent tag that has no children  

```css
# basic syntax 
selector:keyword{ 
    declaration 
}
a:hover{
    color: red;
}
a:active{
    color: orange;
}
a:visited{
    color: purple;
}
```

#### 13. First and Last Child Pseudo Classes

1) This only applies when p tag is first child or last child. If the first child is h1 tag this does not apply.  
2) If you want to apply the style according to first or last child type then goto 14.  

```css
article p:first-child{
    font-weight: bold;
}
article p:last-child{
    color: red;
}
```

#### 14. First & Last of Type Selectors.
This applies to first or last type of child  

```css
article p:first-of-type{
    font-weight: bold;
}
article p:last-of-type{
    color: red;
}
```

#### 15. nth Child Selectors
This applies the style to nth child. It start with 1 not 0.

```css
li:nth-child(1), li:nth-child(7){
    font-weight: bold;
}

li:nth-child(even){
    background: grey;
}
li:nth-child(odd){
    background: pink;
}

li:nth-child(3n + 1){
    color: green;
}
```

#### 16. nth of Type Pseudo Classes
If there is only one selector without descendants at all, nth-child becomes the child of parent tag. First style and Second style sho the same  result.

```css    
article:nth-child(2){
    background: grey;
}
article:nth-of-type(1){
    background: grey;
}
article:nth-of-type(2n + 1){
    background: grey;
}
```

#### 17. Combining Selectors
There should be no space between article and class. If there is no space, it applies the style to all article tags which has class featured-content. If there is a space, it applies it to all descendant's selectors which has featured-content class.

```css
article.featured-content{
    background: red;
}
div.featured-content{
    backgorund: blue
}
```

#### 18. The universal Selector
It targets all selectors directly even a tag(strip off all styles!!). But body tag makes descendants selectors inherit its style indirectly so its style does not apply to a tag.

```css
* {
    color: red
}
```

#### 19. Absolute/Relative Font Size
Relative font size shows the font using em or %. It shows the original font size which is inherited from the parent according to em or %.

```css
article{
    font-size: 16px;
}
article h2{
    font-size: 4em;  // this shows 4 times of original inherited front size 16 which is 64.
}
article p{
    font-size: 500%;  // this shows 500% of original inherited font size 16 which is 90.
}
```

#### 20. Font Family
If first parameter font does not exit then apply next one, if next one does not exist then apply last one.

```css
article h2, article p{
    font-family: arial, helvetica, sans-serif;
}
```

#### 21. Font Weight
Not all font family has bold light option attached to them. !!!!

```css
p{
    font-weight: bold;
    font-family: "Yu Gothic";  // this font family has both light, bold option
}
```

#### 22. Background vs Background-color
background-color just set background color but background can set color, background image using url, etc ...

```css
#header{
    background: #ffffff url("img_tree.png") no-repeat right top;
}
```

#### 23. Styling Links
```css
a{
    color: crimson;
    text-decoration: none;
    font-weight: bold;
}
a:hover{
    color:darkmagenta;
    text-decoration: underline;
    background-color: aquamarine;
}
```

#### 24. Letter Spacing & Line Height
```css
p{
    font-size: 12px;
    line-height: 24px;  // this shows the gap between lines at the size of 12px because upper line only takes 12px.
    letter-spacking: 2em; 
    // this does not inherit parent font size (it normally does) rather than inherit 12px in p tag and times that by two. 
    word-spacing: 0.2em;
}
```

#### 25. The Box Model
![Box Model](/assets/img/posts/box-model.png)

#### 26. Margins / Paddings
1) Set all margins to 30px

```css
.box{
    margin: 30px;
}
```

2) Set same top, bottom margins and same right, left margins

```css
.box{
    margin: 30px 15px;  # top, bottom: 30px  left, right: 15px
    padding: 30px 15px;  # top, bottom: 30px  left, right: 15px
    border: 1px solid #000;
}
```

3) Set top, right, bottom and set left same as right

```css
.box{
    margin: 30px 15px 20px; # left = 15px
    margin: 30px 15px 20px; # left = 15px
}
```

4) Vertical margin collapse : When margins collpase, it takes the larger of the two margins.

5) Set the container in the middle

```css
.box{
    margin: 30px auto;  // auto assigned to right and left margins and center the continer.
}
```

6) Set the container in the middle 2

```css
.box{
    margin: 30px 25%;
    border: 1px solid #000;
    width: 50%;
}
```

#### 27. Block level elements
1) Block level elements take up the whole width of row of its parent, even though you adjust the width of an block level element.  
: p, h1~h6, ol, ul, pre, address, blockquote, dl, div, fieldset, form, hr, noscript, table  
2) Inline level elements does not take up whole row.  
: a, br, button, img, input, label, span, strong, sub, sup, textarea  
3) inline-block level which has merits of inline and block level can be assigned to display selector  

![Box Model](/assets/img/posts/block-inline-level-elements.png)

```css
.block{
    padding: 10px;
    margin: 10px;
    border: 1px solid #000;
    display: inline  // change block level to inline or inline-block level
}
.inline{
    padding: 10px;
    margin: 10px;
    border: 1px solid #000;
    display: inline-block;  // can change inline level to block or inline-block level. 
}
```

**inline-block**

![Inline block](/assets/img/posts/inline-block.png)

#### 28. Width & Height
width and height
The width of an element does not include padding, borders, or margins!

```css
.percentage-width{
    width: 70%;
    height: 50px;
}
.inline-block{
    width: 40%;
    display: inline-block;
}
```

#### 29. Rounded Corners
Use border-radius selector.

```css
.static-width{
    widhth: 300px;
    height: 100px;
    border-radius: 30px;   // get all angle 30px rounded.
    border-radius: 10px 20px;  // top left, bottom right 10px, top right, bottom left 20px rounded
}
```

#### 30. Backgrounds
1) Background without shorthand

```css
.static-width{
    width: 300px;
    height: 300px;
    background-color: #606060;
    background-image: url(https://www.probaka.com/img/ryan.png);
    background-repeat: no-repeat;
    background-position: center;  // can use multiple position as well as percentage
    background-size: 200px;
}
```

2) Background shorthand

```css
.static-width{
    width: 300px;
    height: 300px;
    background: url(https://www.probaka.com/img/aaa.png) no-repeat top center;
    background-color: #606060;
    background-size: 200px;
}
```

3) Multiple backgrounds

```css
#banner{
    background-color: #606060;
    width: 100%;
    height: 300px;
    background-image: url(http://thenetninja.blob.core.windows.net/thenentninja/images/sitewide/logo-white.png),
    url(http://thenetninja.blob.core.windows.net/thenentninja/images/sitewide/home-banner.png);
    background-repeat: no-repeat;   // this is same as no-repeat, no-repeat for 2 urls.
    background-position: center, top left;
}
```

#### 31.Color
1) Hexa code : 6 length code with #. combination of R(2) + G(2) + B(2)  
ex) #000000 : black, #ffffff: white

2) RGB color  
ex) rgb(00, 00, 00) => black, rgb(255, 255, 255) => white

#### 32. Opacity
If there is a text in the selector, text opacity is also affected according to opacity value.  
To prevent this, rgba(100, 200, 200, 0.1) last argument should be used for opacity.

```css
#circle-3{
    width: 400px;
    height: 400px;
    position: absolute;
    background: rgba(100, 200, 200, 0.1);
    border-radius: 200px;
    top:50px;
    left: 250px;
    text-align: center;  // this centers not just text but also image
}
```

#### 33. Gradient
CSS gradients let you display smooth transitions between two or more specified colors.

```css
.button{
    display: block;
    width: 100px;
    padding: 12px;
    border: 1px solid #77aaaa;
    font-family: arial;
    font-weight: bold;
    text-transfrom: uppercase;
    color: #ffff;
    font-size: 14px;
    text-align: center;
    border-radius: 4px;
    background: #aadddd;
    background: linear-gradient(top, #aadddd 0%, #77aaaa 100%);  // from the very top (0%) color starts with #aadddd and transits to #77aaaa to the very bottom (100%) color.
}
```

But, if it does not work because the browser does not support linear-gradient then use vendor prefix.

show background color => if the browser is firefox then apply the style => else if the brower is safari or goole chrome  then apply the style, => if linear-gradient can be applied with our checking vendor prefix apply it right away.

[Gradient](http://colorzilla.com/gradient-editor)

background: #aadddd;  
background: -moz-linear-gradient(top, #aadddd 0%, #77aaaa 100%);  // firefox  
background: -webkit-linear-gradient(top, #aadddd 0%, #77aaaa 100%);  // safari, google chrome  
background: linear-gradient(top, #aadddd 0%, #77aaaa 100%);  

#### 34. Box Shadow
Just use box shadow generator [Box-Shadow](https://www.cssmatic.com/box-shadow)

#### 35. Browse Support
1) Check which browser supports HTML, CSS, javascript [caniuse.com](https://www.caniuse.com)  
2) Makes vendor prefix automatically [pleeease.io](http://pleeease.io/play/)  
3) Provide alternative way using javascript to get around the CSS issues not supported in some browsers. [https://modernizr.com/](https://modernizr.com/)  
4) Fallback Options

```css
.rule{
    background: #ffff;
    background:linear-gradient(top, blue 0%, red 100%);
}
```