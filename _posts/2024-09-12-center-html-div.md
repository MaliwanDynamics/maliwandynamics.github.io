---
layout: post

title: Center Elements In Raw HTML And CSS
imgUrl: /assets/img/post/sept-2024/center-div-head-img.jpg

imgCaption: Center This
imgCaptionSrc: https://www.pexels.com/photo/black-ceiling-wall-161043/

date: 2024-09-12 12:01:00 -0400
categories:
- blog
- software
---
The old “how do I center this f***ing thing” in raw CSS and HTML huh? Well, it's way more simplistic than it seems if you are new to CSS.

To this day, I still do not understand why many resources online make it appear more difficult than it is. I will go into more detail using other methods like grid and flexbox in another post. Keep it simple at first.

## Basic Example

In its most basic form, all you need is a container to put the div inside of, then set the div’s margin to `margin: 0 auto;`

To take it a bit further, create a CSS class so you can easily apply the margin to multiple elements.

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/center-div.png' %}

### The HTML
```html
<head>
    <title>Raw CSS HTML</title>
    <link rel="stylesheet" type="text/css" href="center-div-style.css">
</head>
<body>
    <div class="center-me size-adjusted">
        <p>I am in a centered div!</p>
    </div>

    <div class="not-centered size-adjusted">
        <p>I am NOT in a centered div!</p>
    </div>
</body>
```

### The CSS
```css
.center-me {
    margin: 0 auto;
}
/* Just to make the div visible */
.size-adjusted {
    max-width: 15rem;
    height: 12rem;
}
```

## Full Example With Content Wrapper

You can center more than div elements with the margin auto trick. Here is an example to center everything in the main element. This way you can have a uniform and centered content feel for every page.

As a side note, preference for adding CSS to a main tag in this manner will vary, so I'm not saying this is the best practice, it's just an example. You could add the `.center-me` class to the main element instead (or any element) to avoid duplication.

<a href="https://github.com/MaliwanDynamics/center-div">Full Example On Github</a>

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/center-div-main.png' %}

### The HTML
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Raw CSS HTML</title>
        <link rel="stylesheet" type="text/css" href="center-div-style.css">
    </head>
    <body>
        <main class="main-content">
            <div class="center-me size-adjusted">
                <p>I am in a centered div!</p>
            </div>
    
            <div class="not-centered size-adjusted">
                <p>I am NOT in a centered div!</p>
            </div>
        </main>
    </body>
</html>
```

### The CSS
```css
* {
    margin: 0;
    padding: 0;
}

html {
    width: 100vw;
    height: 100vh;
}

.main-content {

    margin: 0 auto;

    max-width: 900px;
    height: 100%;

    padding-top: 20px;
    padding-bottom: 20px;
    background-color: lightgray;
}

.center-me {
    
    margin: 0 auto;

    background-color: lightgreen;
}

.not-centered {
    background-color: lightcoral;
}

/* Just to make the div visible */
.size-adjusted {
    max-width: 15rem;
    height: 13rem;
}
```