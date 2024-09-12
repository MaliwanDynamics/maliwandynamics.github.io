---
layout: post

title: Center an HTML DIV
imgUrl: /assets/img/post/sept-2024/center-div-head-img.jpg

imgCaption: Center This
imgCaptionSrc: https://www.pexels.com/photo/black-ceiling-wall-161043/

date: 2024-09-12 12:01:00 -0400
categories:
- blog
- software
---
The old “how do I center this f***ing thing” in raw CSS and HTML huh? Well, its a lot more simplistic that it feels at first. To this day, I still do not understand why many resources online make it appear more difficult that it is. I will go into more detail using other methods like grid and flexbox in another post. Keep it simple at first.

## Basic Example

In its most basic form, you just need a container to put the div inside of. Then set the div’s margin to:

```
margin: 0 auto;
```

To take it a bit further, you can create a CSS class to apply the margin to more than just a div tag.

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/center-div.png' %}

### The HTML
```
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
```
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

You can center more than just a div with the margin auto trick. Here is an example to center everything in the main tag. This way you can have a uniform and centered content feel for every page.

(Preference on adding CSS to a main tag will vary, not saying this is always best practice, just an example)

<a href="https://github.com/MaliwanDynamics/center-div">Full Example On Github</a>

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/center-div-main.png' %}

### The HTML
```
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
```
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