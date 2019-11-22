## CSS GRID PROPERTIES

### Container

- grid-template-rows `// grid-template`
- grid-template-columns
- grid-template-areas

* grid-row-gap `// grid-gap`
* grid-column-gap

- justify-items
- align-items
- justify-content
- align-content

* grid-auto-rows
* grid-auto-columns
* grid-auto-flow

### Item

- grid-row-start `// grid-row => grid-area`
- grid-row-end

- grid-column-start `// grid-column => grid-area`
- grid-column-end

- justify-self
- align-self

- order

#### _grid-template-rows_

when you want 2 rows, and height 150px for both of them describe the height of the rows.

`grid-template-rows: 150px 150px;`

#### repeat() function

`grid-template-rows: repeat(2, 150px); // will create 2 row/ tracks with 150px height each`

#### _grid-template-columns_

when you want 3 columns, and width 150px for both of them describe the width of the columns

`grid-template-columns: 150px 150px 150px;`

`grid-template-columns: repeat(3, 150px); // will create 3 columns/ tracks with 150px width each`

`grid-template-columns: repeat(2, 150px) 300px; // will create 2 columns/ tracks with 150px width each and third column track with 300px width`

### The fr unit ( fractional unit)

represents the fraction of the availbale space

`grid-template-columns: repeat(2, 150px) 1fr; // will create 2 columns/ tracks with 150px width each and third column track will occupy all the available space`

If you want all the columns to have same size

`grid-template-columns: repeat(3, 1fr);`
`grid-template-columns: 50% 1fr 1fr;`

### POSITIONING GRID ITEMS

when you want to poistion a grid item/cell at the start of 2nd row and end of 3d row and
at the start of 2nd column and end of 3d column

`grid-row-start: 2;`
`grid-row-end: 3;`
`grid-column-start: 2;`
`grid-column-end: 3;`

##### Shorthand _grid-row/column-start/end_ is _grid-row/column_

`OR => grid-row: 2 / 3; (row start / row end)`
`grid-column: 2 / 3; (column start / column end)`

##### Shorthand FOR _grid-row/column_ is _grid-area_

`OR => grid-area: 2 / 2 / 3 / 3; (row start / column start / row end / column end)`

### SPANNING GRID ITEMS

span grid items across multiple grid cells in order to occupy entire areas.

`grid-column: 2 / 4;`

So if we have more items than we actually define cells, then CSS grid will automatically
add a new row or a new column.
And this part (new row or new column) is then called an implicit grid.

Actually we can have multiple grid item in the same cell.
when we will define explicitly the positions of the grid items, if some of the elements are
positioned in th same cells then the grid items will get overlapped/ hidden.
And if you want the hiiden items to be displayed then give a higher z-index.

`OR => grid-column: 1 / span 2; // it will span across 2 cells`

`OR => grid-column: 1 / -1; // if you don't know how many columns to span, all you know is till end then '-1' will do the job`

### NAMING GRID LINES

#### Method 1: **LINE NUMBERS**

#### Method 2: **LINE NAMES**

```
grid-template-rows: [header-start] 100px [header-end box-start] 200px [box-end main-start] 400px
                    [main-end footer-start] 100px [footer-end];
```

```
grid-template-columns: repeat(3, [col-start] 1fr [col-end]) 200px [grid-end];
```

- for 1st column track => col-start 1 and col-end 1
- for 2nd column track => col-start 2 and col-end 2
- for 3rd column track => col-start 3 and col-end 3

`"we can give one line more than one names."`

**> USE: grid-row: box-start / main-end**

#### Method 3: **NAME GRID AREAS**

- we'll give each grid cell a name.
- let we have 4 X 4 grid
- so we'll give first 4 cells 4 names

`grid-template-areas: "head head head head" // all the 4 cells represent head`
`"box-1 box-2 box-3 side"`
`"main main main side"`
`"foot foot foot foot";`

like 4 X 4 grid you have to give names to 16 cells otherwise it would not work properly.

`if you want some empty cells then put a dot(.) instead`

`grid-template-areas: "head head head ."`
`"box-1 box-2 box-3 side"`
`"main main main side"`
`"foot foot foot foot";`

`For positioning items:- grid-area: head; // name of the area.`

### IMPLICIT GRIDS VS EXPLICIT GRIDS

**EXPLICIT GRID**: When we expicitly define how rows and columns of a grid should look like then it is known as explicit grid.

**IMPLICIT GRID**: If we have more grid items than space, then CSS grid automatically adds some more tracks to the grid
in order to fit all of the remaining items.

#### Style Implicit Grids

`grid-auto-rows: 80px; // In the automatically created implicit grid, rows will have height of 80px.`

`grid-auto-flow: row/ column; // default is row.`

`the implicit grid will be added/placed as rows by default if grid-auto-flow is set to columnthen it will be added as columns.`

`grid-auto-columns: .5fr; // it can be set only after grid-auto-flow is set to column.`

## ALIGNING GRID ITEMS TO GRID AREAS

`align-items: center / start / end / stretch; // deafult is stretch`

align the items across the column axis (vertically) inside the grid area.

`justify-items: center / start / end / stretch; // deafult is stretch`

align the items across the row axis (horizontally) inside the grid area.

#### FOR SINGLE GRID ITEM TO OVERRIDE THE ALIGNING PROPERTIES OF THE GRID CONTAINER -

`align-self: center / start / end / stretch;`

align the item across the column axis (vertically) inside the grid area.

`justify-self: center / start / end / stretch;`

align the item across the row axis (horizontally) inside the grid area.

### ALIGNING GRID TRACKS TO GRID CONTAINER

`align-content: center / start / end / space-between / space-around / space-evenly;`

align the tracks inside the container across the column axis (vertically).

`justify-content: center / start / end / space-between / space-around / space-evenly;`

align the tracks inside the container across the row axis (horizontally).

The automatic placement algorithm, it tries to keep the grid items that we have in order, so it tries to follow that order.
And so sometimes, that can create kind of holes in the grid conatiner (empty grid cells),
but if we want to fix that, we can actually do it

`grid-auto-flow: row dense; // creates dense grid with no holes.`

### MIN-CONTENT, MAX-CONTENT AND MINMAX()

`grid-template-rows: repeat(2, min-content);`

`grid-template-columns: max-content 1fr 1fr min-content;`

- **_max-content_**: the largest content that we have in the 1st column becomes the width of the entire column
  without causing to make any line breaks in the content.

- **_min-content_**: takes the largest width that is needed to fit the content without overflowing.

- **_minmax(100px, 200px)_**: we pass two values in and then CSS ensures that the track will always stay between these two values.

`grid-template-rows: repeat(2, minmax(150px, min-content));`

`The CSS Grid specification says that a fractional unit fills up the entire remaining space but it is never smaller than the minimum content of a row or a column.`

### AUTO-FIT AND AUTO-FILL - RESPONSIVE LAYOUTS

`grid-template-rows: repeat(2, minmax(150px, min-content));`

when do don't know how many columns or rows you need to create. Example-

`grid-template-columns: repeat(auto-fill, 1fr);`

Example - Suppose grid container has width = 1000px and
we have defined auto-filled the columns ( assuming 8) with width = 100px each.

`grid-templates-rows: repeat(auto-fill, 100px);`

`Here CSS Grid will automatically create 10 tracks (1000/ 100 = 10 tracks)`

- **_auto-fill_**: it automatically creates as many tracks with the desired width that we specify here
  as fit into the container.

- **_auto-fit_**: auto-fit does is that it actually collapses these tracks and gives it a width of zero, creating then this extra space that we see here.
  So, it creates these tracks (8 columns), and then leaves the empty space,
  which we can then fill, if we want it.
