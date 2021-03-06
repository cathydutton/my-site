---
title: Sass dynamic colour change
author: Cathy Dutton
layout: external-post
category: post
---
When building the website for <a href="http://get-maze.co.uk/" target="_blank">Maze</a> I wanted to display the content on one page with a downward scroll. Each section or slide would therefore need to have a different background colour to emphasise the content change.

To achieve this I took advantage of some of the new features in Sass. Firstly using variables I was able to store my colour values&#8230;

```
$orange: #ffa600;
$blue: #82d2e5;
$green:#c1d72e;
$light-grey: #b2b2b2 ;
$dark-grey: #5e5e5e ;
```

I then used a list to assign a colour variable to each slide in the site&#8230;

```
$color :
(1, $orange),
(2, $blue),
(3, $green),
(4, $light-grey),
(5, $dark-grey);
```

An @each loop is then used to run through the list and generate the css for each slide.

```
@each $number, $bg in $color {

  .slide-#{$number} {
    background:$bg;
  }

}
```

The loop generates the css code for each slide takeing the relavant value for $bg from the $color list.

```
.slide-1 {background: #ffa600;}
.slide-2 {background: #82d2e5;}
.slide-3 {background: #c1d72e;}
.slide-4 {background: #b2b2b2;}
.slide-5 {background: #5e5e5e;}
```

A working example can be found on <a href="http://codepen.io/cathydutton/pen/ndfHh" target="_blank">Codepen </a>
