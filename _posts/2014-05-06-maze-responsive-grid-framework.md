---
title: 'Maze &#8211; responsive grid framework'
author: Cathy Dutton
layout: post
category: post
---
After numerous rants regarding my disliking for Bootstrap and most other front end frameworks, I decided to have a go myself. The results can be found here <a href="http://www.get-maze.co.uk" target="_blank" >www.get-maze.co.uk</a>, an easy to customise grid built using Sass and HTML 5. My aim with Maze was to produce a simple to use set of mixins enabling percentage widths to be assigned to any selector in any layout.

<h2 class="heading">Why?</h2>

I decided to build the framework for two main reasons. Firstly to get up to speed with Sass, and secondly to address some of the common issues I have with a lot of the grids already out there. Some of these issues are listed below&#8230;

<ul class="list">
  <li>
    <strong>Presentational class names</strong> &#8211; Such as span-1 or large-9.columns are used instead of more semantic selectors.
  </li>
  <li>
    <strong>Full width defaults</strong> &#8211; All elements default to full width at tablet view creating extra long websites that could be better arranged.
  </li>
  <li>
    <strong>Set  breakpoints</strong> &#8211; Set media queries and column numbers make the systems to rigid.
  </li>
  <li>
    <strong>Excess class names</strong> &#8211; Extra class names need to be added to style the content of div&#8217;s using the same layout style.
  </li>
  <li>
    <strong>Style guides and library includes</strong> &#8211; Unnecessary functionality creates bloat.
  </li>
</ul>

My goal was to create a more adaptable grid, using Sass variables and formulae to enable complete customisation. I also wanted to create a more stripped back framework with no style elements or library&#8217;s.

<h2 class="heading">Customisable Code</h2>

The number of grid columns, push value and gutter width can be easily changed by editing the variables shown below. The percentage width of a single column span is created using the $grid-columns value and assigned to the variable $unit.

```
$grid-columns: 12;
$unit: (100%  / $grid-columns);
$gutter: 2% !default;
$push: 0 !default;
```

A Sass mixin is used to output the grid CSS. Each elements width is calculated using the values passed from the variables described above and user inputted values for the required column span ($col) and float direction ($fold). the $fold variable determines whether the columns will collapse from the right or the left as the grid is re-sized. By default the right column will move to a new row, setting a value of $fold:right will move the left column.

```
@mixin grid($col, $fold:"left", $push:$push, $margin:$gutter) {
  @include transition;
  float:#{$fold};
  background: $base-color;
  cursor: pointer;
  padding: 20px;
  width: (($unit * $col) - $margin ) + ( $margin / ( $grid-columns / $col) );

  @if $push &gt; 1 {
    margin-left: (($unit * $push) ) + ( $gutter / ( $grid-columns / $push) );
  }

  @if $fold == left {
    margin-right: $margin;

    &:last-child {
      margin-right: 0;
    }

  }

  @if $fold == right {
    margin-left: $margin;

    &:last-child {
      margin-left: 0;
    }

  }

  &:hover {
    background: $brown;
    color: $white;
  }

}
```

<h3 class="heading">How</h3>

Firstly a single span column width is calculated and stored in a new variable $unit&#8230;

```
$unit: (100%  / $grid-columns);  
```

If we have a 12 column grid then a single span column will be (100% / 12) which is equal to 8.333%. This value is used to generate the percentage widths of any column span&#8230;

```
width: (($unit * $col) - $gutter ) + ( $gutter / ( $grid-columns / $col) );
```

In our example $unit is equal to 8.333%, $grid-columns is equal to 12 and $gutter is equal to 2%. To find the width for an element spanning 5 columns the formulae would be&#8230;

```
width: ((8.333 * 5) - 2 ) + ( 2 / ( 12 / 5) );  //  which equals  40.5%
```

The width for a 5 column span would therefore be 40.5%. The first part of the formulae calculates the width by multiplying the value for one span by the desired span and removing the gutter value. The second part of the formulae adds to the width to compensate for the missing gutter value which is not applied to the last child in each row. (see below code)

```
&:last-child {
  margin-right: 0;
}
```

The gutter percentage is set using the variable $gutter. This value is used throughout the site build for all column margins. If a layout uses multiple margin values the $gutter variable can be over-ridden using the mixin.

```
.logo {
  @include grid(3); // Default, uses the variable $gutter value
  @include grid(3, $margin:0);  // Sets margin to 0
  @include grid(3, $margin:4%);  // Sets margin to 4%
}   
```

The mixin adds the gutter value to a margin property dependant on the value of the $fold variable. If $fold is set to left, (the default option) then a margin-right is applied to all elements except the last child, the right column will be moved to the row below as the grid is re-sized. If $fold is set to right, a margin-left is applied to all elements except the last child, the left column will then be moved to the row below as the grid is re-sized.

```
@if $fold == left {
  margin-right: $gutter;

  &:last-child {
    margin-right: 0;
  }

}  

@if $fold == right {
  margin-left: $gutter;

  &:last-child {
    margin-left: 0;
  }

}
```

If a push value is set a margin-left is added to that element using this part of the formulae&#8230;

```
@if $push &gt; 1 {
  margin-left: (($unit * $push) ) + ( $gutter / ( $grid-columns / $push) );
}
```

The mixin in full is written below, the full grid set up can be viewed here <a href="http://www.get-maze.co.uk/maze/" target="_blank"> Maze demo</a>

```
@mixin grid($col, $fold:"left", $push:$push, $margin:$gutter) {
  @include transition;
  float:#{$fold};
  background: $base-color;
  cursor: pointer;
  padding: 20px;
  width: (($unit * $col) - $margin ) + ( $margin / ( $grid-columns / $col) );

    @if $push &gt; 1 {
      margin-left: (($unit * $push) ) + ( $gutter / ( $grid-columns / $push) );
    }

    @if $fold == left {
      margin-right: $margin;

      &:last-child {
        margin-right: 0;
      }

    }

    @if $fold == right {
      margin-left: $margin;

      &:last-child {
        margin-left: 0;
      }

    }

    &:hover {
      background: $brown;
      color: $white;
    }

}
```

<h3 class="heading">Responsive</h3>

The media queries used in maze are also added to each selector using @include. This allows for media queries to be kept in line with the desktop styles making them easier to manage.

Firstly the break points are stored as variables&#8230;

```
$break-wide: 1240px;
$break-desktop: 990px;
$break-tablet: 767px;
$break-mobile: 480px;
```

The media query mixin has two arguments $media and $width, allowing the column span to be edited at the desired points.

```
@mixin break($media, $col) {
	@if $media == tablet {
		@media only screen and (max-width:$break-tablet) {
			width: (($unit * $col) - $gutter ) + ( $gutter / ( $grid-columns / $col) );
			margin: $gutter / 2;
			margin-left: 0;
		}
	}
	@else if $media == mobile {
		@media only screen and (max-width:$break-mobile) {
			width: (($unit * $col) - $gutter ) + ( $gutter / ( $grid-columns / $col) );
			margin: $gutter / 2;
		}
	}
}
```

Finally by using @include the selectors are free from presentational classes and can adopt any naming convention.

```
.logo {
  @include grid(3);
  @include break(tablet, 6);
  @include break(mobile, 12);
}
```

<h3 class="heading">Benefits</h3>

**Semantics**- Maze removes the need to add unfriendly classes to your mark-up, and allows for cleaner semantic naming conventions. This in turn ensures sites scalable and easy to maintain.

**Control** &#8211; A common practice in responsive web design is to set each element to 100% at either the tablet or mobile break point. Maze allows for full control over the re-sizing of each HTML block allowing the content to respond as and where needed.

**Customise** &#8211; Using the existing media query mixins and variables as a guide any number of break points can be created ensuring the site is fully fluid. Maze will work for 8, 12 & 16 column layouts, and has an easily adjustable gutter width percentages.
