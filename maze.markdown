---
layout: maze
title: "Maze - PostCSS responsive grid"
description: "A Simple mobile first responsive Grid built with PostCSS"
intro: "Maze"
heading: " A fully flexible mobile first grid to suit any design pattern."
group: "navigation"
page: "PostCSS Maze"
active: "PostCSS Maze"
---


<section>
		<p>Maze is a flexible and semantic mobile first responsive grid built with PostCSS. Maze is fully customisable and removes the reliance on .last-column classes by instead applying the margin to both sides of each element and adjusting the wrapper width accordingly.</p>
		<p><a href="http://cathydutton.github.io/postcss-maze/" title="Demo of Maze PostCSS grid">View a demo of Maze</a></p>
		<p><a href="https://github.com/cathydutton/postcss-maze" title="Maze source code on Github">View the source code for maze on Github</a></p>
</section>


<section>
		<h2>Installation</h2>
<pre>
npm install postcss-maze
</pre>

		<h2>Creating a grid</h2>
		<p>Firstly the wrapper is given a property of grid-container with a value of true...</p>

<pre>
.wrapper {
  grid-container: true;
}
</pre>

		<p>This calculates the wrapper width based on the values assigned to the largest and smallest media queries, and adds a clearfix.</p>

		<p>The max width is calculated accounting for the element margins...</p>

<pre>
.wrapper {
  max-width: 1030.2px;
  min-width: 260px;
  margin: 0 auto;
  box-sizing: border-box;
}

.wrapper::after {
  content: "" ;
  display: table;
  clear: both;
}
</pre>

		<p>Each element is then created as a ratio at a set media query...</p>

<pre>
.four-elements {
  col-span: mobile(1,1);
  col-span: phablet(1,2);
  col-span: tablet(1,4);
}
</pre>

<pre>
.four-elements {
  float: left;
  box-sizing: border-box;
  margin-right: 0.5%;
  margin-left: 0.5%;
  width: 99%;
}

@media only screen and (min-width:30em) {

  .four-elements {
    width: 49%;
  }

}

@media only screen and (min-width:48em) {

  .four-elements {
    width: 24%;
  }

}
</pre>

		<p>The above element will display one per row at mobile, two per row at landscape and 4 per row at tablet. The Mobile declaration is the default value and therefore is not rendered inside a media query.</p>


	<h3>Examples</h3>

<pre>
.twelve-elements {
  col-span: mobile(1,1);
  col-span: phablet(1,2);
  col-span: tablet(1,4);
  col-span: desktop(1,6);
  col-span: wide(1,12);
}
</pre>

<pre>
.six-elements {
  col-span: mobile(1,2);
  col-span: tablet(1,3);
  col-span: desktop(1,6);
}
</pre>


		<h3>Settings</h3>

		<p>By default Maze works with 5 media queries and has a margin of 1%. These settings can be overridden with custom config. All media query dimensions should be written in EM's, and margins as a percentage...</p>

<pre>
var processors = [
  postcssmaze({
    media: {
      mobile:    20,
      phablet:   30,
      tablet:    48,
      desktop:   63.750,
      wide:      80
    },
  settings: {
    margin: 10
  }
}),
</pre>

	<p>An example using Gulp as a task runner...</p>

<pre>
// CSS TASK
gulp.task('css', function () {
 var concat = require('gulp-concat'),
 postcss = require('gulp-postcss'),
 mqpacker = require('css-mqpacker'),
 postcssmaze = require('postcss-maze'),
 autoprefixer = require('autoprefixer');

 var processors = [
  postcssmaze({
   media: {
   mobile:    20,
   phablet:   30,
   tablet:    48,
   desktop:   63.750,
   wide:      80
  },
  settings: {
   margin: 10
  }
 }),
 mqpacker,
 autoprefixer({
  browsers: ['> 2%', 'IE >= 9', 'iOS >= 7'],
  cascade:  false,
  map:      true,
  remove:   true
 })
];

 return gulp.src('src/layout.css')
 .pipe(postcss(processors))
 .pipe(concat('dist/output.css'))
 .pipe(gulp.dest('.'));
});

</pre>
</section>
