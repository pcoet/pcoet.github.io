---
date: 2020-04-11
categories:
  - CSS
  - web development
---

# An intro to grids

This post provides an introduction to the [CSS grid layout](https://www.w3.org/TR/css-grid-1/). The CSS grid is a powerful tool with a lot of functionality, much of which we won't cover here. We'll just cover enough basics so that you can start working with grids, and you'll know where to find additional info. We'll also take a look at the [Bootstrap grid system](https://getbootstrap.com/docs/4.4/layout/grid/), since that's what many devs actually use for their layout.

Note: If you're planning to use the CSS grid in production, you should check the [current browser support](https://caniuse.com/#feat=css-grid). At the time of this writing (April 2020), CSS Grid Layout is fully supported by all the major browsers in active development. IE partially supports an older version of the specification, and Opera Mini doesn't support it at all.

## What is the CSS grid?

The CSS grid is a two-dimensional layout that lets you arrange elements on the page into rows and columns. It's like a table, but more flexible. Using media queries, you can adjust the grid layout for different devices and viewport widths. [Flexbox](https://www.w3.org/TR/css-flexbox-1/) solves similar problems, but it does so on a one-dimensional axis &mdash; either horizontal or vertical. The grid lets you specify alignment across the entire two-dimensional space.

If you're new to web development, you may have missed out on the "bad old days" when developers had to use the [float](https://developer.mozilla.org/en-US/docs/Web/CSS/float) property to create flexible layouts. You could make it work, but it was an involved process, and it wasn't especially intuitive. (Chris Coyier's [All About Floats](https://css-tricks.com/all-about-floats/) provides a great overview of the uses and shortcomings of floats.) Grid and flexbox address the shortcomings of float-based layouts.

## A simple example

Let's look at a simple example grid.

<p class="codepen" data-height="400" data-theme-id="light" data-default-tab="css,result" data-user="pcoet" data-slug-hash="VwLogve" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Simple grid">
  <span>See the Pen <a href="https://codepen.io/pcoet/pen/VwLogve">
  Simple grid</a> by pcoet (<a href="https://codepen.io/pcoet">@pcoet</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Here we have 6 div elements laid out on a 2x3 grid. The properties that we care about are:

* [display](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
* [grid-template-columns](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns)
* [grid-template-rows](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-rows)

The `display` property is set to `grid`, which tells the browser that we want to use a grid layout. `grid-template-columns` defines the column size for our layout. Here It's set to `1fr 4fr 1fr`, which indicates the fraction (`fr`) of the grid container's column axis that each column should take. The `fr` unit indicates a proportion. In this case, we have (1 + 4 + 1 = ) 6 parts total, so the left column takes up 1/6 of the grid, the middle column takes up 2/3 of the grid, and the right column takes up 1/6 of the grid. `grid-template-rows` defines our row size, `100px 200px`, indicating that the first row should take up 100px on the vertical axis, and the second row should take up 200px. We could also have used the `fr` unit for our rows, or we could have mixed `px` and `fr` units.

Using these three properties, we've created a grid layout that is visually divided by column tracks and row tracks. We explicitly specified three columns and two rows, and that's what we see. As an experiment, you can [edit the code above](https://codepen.io/pcoet/pen/VwLogve) and try adding the following as the last child of the grid wrapper element: `<div>Seven</div>`. This new element will line up under the first column in a new third row, spanning as much of the row as it needs to display its content, but no more. This element is part of the implicit grid. We didn't define a row for it using `grid-template-rows`, but the grid aligns it with the existing row and column lines.

## A more interesting example

In creating an actual web design, we probably want something more complex than the above example. For instance, we might want to have header and footer elements that span the entire column axis of the containing grid. We can create such a design using the [grid-column-start](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column-start) and [grid-column-end](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column-end) properties.

<p class="codepen" data-height="500" data-theme-id="light" data-default-tab="css,result" data-user="pcoet" data-slug-hash="PoPojrV" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Grid with header and footer">
  <span>See the Pen <a href="https://codepen.io/pcoet/pen/PoPojrV">
  Grid with header and footer</a> by pcoet (<a href="https://codepen.io/pcoet">@pcoet</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Notice the `header` and `footer` classes, which set `grid-column-start` to 1 and `grid-column-end` to 4. What we're doing here is telling the browser that these columns should start at the first grid line and end at the fourth grid line. (Note that the lines are indexed starting at 1.) Grid lines are the lines between row and column tracks. Using `grid-template-columns`, we've defined three columns. Three columns have four lines. So to create an element that spans the entire width of the grid, we have to have it span from the first line (1) to the last line (4). If we wanted to define an element that spanned rows, we'd use [grid-row-start](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-row-start) and [grid-row-end](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-row-end). These can be combined, so that you define an element that spans both columns and rows. There are also shorthand and default ways of expressing `-start` and `-end` properties and values, as explained in [MDN: Line-based placement with CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Line-based_Placement_with_CSS_Grid).

## The Bootstrap grid

The Bootstrap grid handles the layout for many websites out in the wild. It's worth noting that the Bootstrap grid is actually implemented with flexbox, but it's designed to solve many of the same problems as the CSS grid. With a small amount of cutting and pasting, you can have a fluid layout that looks great across devices and browser widths. But to get the most benefit out of Bootstrap, you need to understand how the 12-column [Bootstrap grid system](https://getbootstrap.com/docs/4.4/layout/grid/) works.

Probably the most important things to understand is how to use classes to configure the grid. The official documentation on [grid options](https://getbootstrap.com/docs/4.4/layout/grid/#grid-options) and [responsive classes](https://getbootstrap.com/docs/4.4/layout/grid/#responsive-classes) is a good place to start, and we'll expand on that here. 

To use the Bootstrap grid, you set predefined CSS classes in your HTML. Here's a simple example, with one row and three columns.

<p class="codepen" data-height="350" data-theme-id="light" data-default-tab="html,result" data-user="pcoet" data-slug-hash="JjYodpq" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Bootstrap grid">
  <span>See the Pen <a href="https://codepen.io/pcoet/pen/JjYodpq">
  Bootstrap grid</a> by pcoet (<a href="https://codepen.io/pcoet">@pcoet</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

If you [view the full page](https://codepen.io/pcoet/full/JjYodpq) in a browser and resize the viewport, you'll notice that the columns don't restack on the page, no matter how narrow you make it. Not a very responsive grid. What's happening here? We haven't defined any breakpoints. 

The `col` class can be modified to define breakpoints using the following size postfixes: `-xs` (<576px), `-sm` (&ge;576px), `-md` (&ge;768px), `-lg` (&ge;992px), and `-xl` (&ge;1200px). You specify a breakpoint by appending the size to the column class, like this: `col-sm`. If we change all of our `col` classes to `col-sm` and then resize the viewport down to less than 576px, we see our columns start to stack. If we use `col-md`, the columns start to stack at less than 768px. If we don't append a size, Bootstrap defaults to `-xs`, which means that the column layout will be applied at less than 576px. Bootstrap's grid system applies breakpoints to all viewport widths above the specified breakpoint, so if you set `-xs`, even by default, you're effectively telling Bootstrap not to restack your columns, no matter how small the width of the screen. The best way to get a feel for these breakpoints is to play with them in the browser.

Let's look at a slightly more complex grid that takes advantage of Bootstrap's 12-column layout. We can combine breakpoints and column numbers to make a layout that's both precise and flexible.

<p class="codepen" data-height="500" data-theme-id="light" data-default-tab="html,result" data-user="pcoet" data-slug-hash="VwvYEzJ" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Bootstrap grid with column numbers">
  <span>See the Pen <a href="https://codepen.io/pcoet/pen/VwvYEzJ">
  Bootstrap grid with column numbers</a> by pcoet (<a href="https://codepen.io/pcoet">@pcoet</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Notice that the `col` classes now include two postfixes, e.g. `col-md-3`. The size postfix (`-md`) tells Bootstrap that the grid layout should apply when the viewport width is at or above a certain size (here 768px). The number (`-3`) indicates the number of columns on the 12-column grid that the div should span. In this case, our first row divides the available columns into a 3-column and a 9-column layout, and our second row divides the available columns into 3 4-column divs. If you [view the full page](https://codepen.io/pcoet/full/VwvYEzJ) and adjust the viewport width down to 767px or less, you can see the columns stack.

## Takeaways

This post is just an intro to working with CSS grids. There's a lot more to know! To become proficient with modern CSS layouts, you'll also need to understand [flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox) and [responsive design](https://developers.google.com/web/fundamentals/design-and-ux/responsive), at a minimum. If you're interested in the history of the grid specification, you might also check out [The Story of the CSS Grid, from Its Creators](https://alistapart.com/article/the-story-of-css-grid-from-its-creators/).

One question that often comes up in discussions of responsive design is whether you should create your own layout or use Bootstrap (or another CSS framework). This really depends on the use case. There are reasons that you might not want to have a dependency on Bootstrap, including the concern that other sites already have a "Bootstrap-y" look. But my tendency is to use Bootstrap, unless there's a reason not to. You can get a unique look by adding your own styles on top of Bootstrap, and duplicating the functionality and reliability of the Bootstrap grid across browsers will take a non-trivial amount of work. At a certain point, the issue is similar to using standard libraries in a programming language. Yes, you could write your own sorting utilities, and, yes, it's helpful if you know how they work. But building on the work of other developers frees you up to solve other problems.

## Additional Resources

* [CSS-Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [MDN: Basic Concepts of grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
* [MDN: CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
* [MDN: Glossary: Grid](https://developer.mozilla.org/en-US/docs/Glossary/Grid)
* [MDN: Relationship of grid layout to other layout methods](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Relationship_of_Grid_Layout)