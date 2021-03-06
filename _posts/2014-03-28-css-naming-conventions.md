---
title: 'What&#8217;s in a name'
author: Cathy Dutton
layout: post
category: post
---
Back when front end frameworks like Foundation were built using css instead of Sass the class names were presentational as opposed to semantic. The mark up used in grid systems was similar to the code example below.</p>

<pre class="wp-code-highlight prettyprint">&lt;div class="row"&gt;
  &lt;div class="small-2 large-4 columns"&gt;...&lt;/div&gt;
  &lt;div class="small-4 large-4 columns"&gt;...&lt;/div&gt;
  &lt;div class="small-6 large-4 columns"&gt;...&lt;/div&gt;
&lt;/div&gt;</pre>

This code is neither user friendly or descriptive of the elements inside each div. Extra classes would also need to be added to provide the unique styling for each element.

Now thanks to Sass and in particular placeholders and mixins, class names can remain semantic and pull in the correct grid reference styles. This helps to keep sites maintainable and reduces the number of div&#8217;s and classes in the mark up.

The code example below shows more readable code which is much simpler to maintain and grow.

```
.logo {
@include grid(3,  0);
@include break(tablet, 50%);
@include break(mobile, 100%);
}
.search {
@include grid(6,  0);
@include break(tablet, 50%);
}
.social-share {
@include grid(3,  0);
@include break(tablet, 100%);
}
```

<h2 class="heading"> Colours</h2>

If we have a heading which needed to be displayed in red, a descriptive selector would be .red, this however would create extra work should the colour ever change. To avoid having to update the hex colour value and the HTML selector we can call the class by a different name and use variables to set the colour scheme.

Example selectors include&#8230;

```
.emphasis
.link-colour
.brand-colour
```

Using a base.scss file colours can be set up and stored in varaibles, these variables are then assigned to more semantic selectors used throughout the site. The code below allows for any colour to be changed by editing just one file&#8230;

```
/* COLOUR DEFAULTS
========================================================================== */

/* Colours -  Defined only once */
$orange: #ffa600;
$green: #c1d72e;
$blue: #82d2e5;
$red: #FF0000;
$white: #fff;
$black: #000;
$grey: #333;
$light-grey:#ececec;

/* Mark-up - selectors used throughout site. */
$base-color: $orange;
$secondary-color: $green;
$tertiary-color: $grey;
$accent-color: $blue;
$error-color: $blue;
```

An example of the code used above can be found on <a href="https://github.com/cathydutton/bear/blob/master/src/sass/base/_base.scss" target="_blank">GitHub</a>.
