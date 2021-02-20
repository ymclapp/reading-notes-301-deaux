# CSS GRID

Another item that has a lot of information and so many different ways to do the CSS grid.  I found many sites to guide a CSS grid.

Some of them I found are:
https://www.w3schools.com/cssref/pr_grid.asp
https://css-tricks.com/dont-overthink-it-grids/
https://www.w3schools.com/css/css_grid.asp
https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout
    - Like tables, grid layout enables an author to align elements into columns and rows. However, many more layouts are either possible or easier with CSS grid than they were with tables. For example, a grid container's child elements could position themselves so they actually overlap and layer, similar to CSS positioned elements.

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout
A grid is a set of intersecting horizontal and vertical lines defining columns and rows. Elements can be placed onto the grid within these column and row lines. CSS grid layout has the following features:

### Fixed and flexible track sizes
You can create a grid with fixed track sizes – using pixels for example. This sets the grid to the specified pixel which fits to the layout you desire. You can also create a grid using flexible sizes with percentages or with the new fr unit designed for this purpose.

### Item placement
You can place items into a precise location on the grid using line numbers, names or by targeting an area of the grid. Grid also contains an algorithm to control the placement of items not given an explicit position on the grid.

### Creation of additional tracks to hold content
You can define an explicit grid with grid layout. The Grid Layout specification is flexible enough to add additional rows and columns when needed. Features such as adding “as many columns that will fit into a container” are included.

### Alignment control
Grid contains alignment features so we can control how the items align once placed into a grid area, and how the entire grid is aligned. 

### Control of overlapping content
More than one item can be placed into a grid cell or area and, they can partially overlap each other. This layering may then be controlled with the z-index property.

Grid is a powerful specification that, when combined with other parts of CSS such as flexbox, can help you create layouts that were previously impossible to build in CSS. It all starts by creating a grid in your grid container.

### Grid Tracks
We define rows and columns on our grid with the grid-template-columns and grid-template-rows properties. These define grid tracks. A grid track is the space between any two lines on the grid. In the below image you can see a track highlighted – this is the first row track in our grid.

### The fr Unit
Tracks can be defined using any length unit. Grid also introduces an additional length unit to help us create flexible grid tracks. The new fr unit represents a fraction of the available space in the grid container. The next grid definition would create three equal width tracks that grow and shrink according to the available space.

