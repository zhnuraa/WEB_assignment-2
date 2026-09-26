# Assignment #2 — Defense Preparation

**Student:** Nurasyl Zhumagul  
**Course:** WEB Technologies 1 (Front End)

This guide explains the layout techniques used in `index.html` and `style.css`. During the defense, open the CSS next to the browser and identify the selectors before changing a property.

## 1. What is Flexbox?

Flexbox is a CSS layout system for arranging elements in one main direction: a row or a column. It helps distribute space, align items, and let items grow or shrink. This project uses it for navigation, the three-card row, and the content inside cards.

## 2. What is CSS Grid?

CSS Grid is a layout system that arranges elements in rows and columns. It is useful when both dimensions matter. This project uses Grid for the page-layout demonstration, the image gallery, and the portfolio columns.

## 3. What is the main difference between Flexbox and Grid?

Flexbox primarily controls one dimension at a time: a row or a column. Grid controls rows and columns together. Flexbox can wrap onto several lines, but each line distributes its own space; Grid can keep items aligned to shared column and row tracks.

## 4. What is the main axis in Flexbox?

The main axis is the direction in which Flexbox lays out its items. `flex-direction` determines that direction. In this English, left-to-right page, `row` gives a horizontal main axis, and `column` gives a vertical main axis. `justify-content` works along the main axis.

## 5. What is the cross axis?

The cross axis is perpendicular to the main axis. For `flex-direction: row`, the cross axis is vertical. For `flex-direction: column`, it is horizontal. `align-items` controls how the items align along this cross axis.

## 6. What does `display: flex` do?

It makes an element a flex container. Its direct children become flex items. For example, setting it on `.cards-container` lets the three cards share a row. It does not automatically turn every nested descendant into a flex item.

```css
.cards-container {
    display: flex;
}
```

## 7. What does `justify-content` do?

It distributes available space along the main axis. In a row, `center` centers the items horizontally, while `space-between` places the first and last items at opposite edges and distributes the remaining space between them. The navbar uses `space-between` to separate the logo from the links. In a column, the same property works vertically instead.

## 8. What does `align-items` do?

It aligns items along the cross axis. In the row-based navbar, `align-items: center` vertically centers the logo and menu. `stretch` makes eligible items fill the available cross-axis size; it is used to give the desktop cards equal height. In a column layout, `align-items: center` centers items horizontally.

## 9. What does `flex-direction` do?

It chooses the main-axis direction. The default is `row`. This project uses `column` inside cards so the image, heading, description, and action follow each other vertically. A media query also changes the outer card row to a column on smaller screens.

```css
.card {
    display: flex;
    flex-direction: column;
}
```

## 10. What does `gap` do?

`gap` creates consistent space between Flexbox or Grid items. It does not add padding around the outside of the container. One value sets both row and column gaps; two values set the row gap first and the column gap second.

```css
.cards-container {
    gap: 24px;
}
```

## 11. What does `flex: 1` mean?

It is shorthand for allowing an item to grow and shrink with a zero starting basis; browsers commonly expand it to `flex: 1 1 0%`. Sibling cards with `flex: 1` share the available row width equally when their minimum-size constraints allow it. It gives equal width here, while the parent's cross-axis stretching gives equal height. It does not mean “one pixel.”

## 12. What does `display: grid` do?

It makes an element a grid container. Its direct children become grid items. Properties such as `grid-template-columns`, `grid-template-rows`, and `grid-template-areas` then define how those children are arranged.

## 13. What does `grid-template-columns` do?

It defines the number and sizes of explicit Grid columns. This example creates a `240px` sidebar column and a flexible main column:

```css
.grid-layout {
    grid-template-columns: 240px 1fr;
}
```

The portfolio instead uses `2fr 1fr`, so the left column gets twice the available flexible space of the right column, after the gap is accounted for.

## 14. What does `grid-template-rows` do?

It defines the number and sizes of explicit Grid rows. The Grid Areas demonstration uses:

```css
.grid-layout {
    grid-template-rows: auto 1fr auto;
}
```

The header and footer rows size according to their content. The middle flexible row receives available space when the container has extra height. With no extra constrained height, the content still determines how tall the layout needs to be; `1fr` does not automatically make it fill the screen.

## 15. What does `grid-template-areas` do?

It names regions of a grid and describes their arrangement. Each quoted line is a row, and each name in that line occupies a column cell. Repeated names create one larger rectangular area.

```css
.grid-layout {
    grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
}
```

Here, the header spans both columns, the sidebar and main share the middle row, and the footer spans both columns. All rows must contain the same number of cells, and a repeated named area must form a rectangle.

## 16. What does `grid-area` do?

In this project, it assigns a grid item to a name declared by `grid-template-areas`. The spelling must match the area name.

```css
.grid-header { grid-area: header; }
.grid-sidebar { grid-area: sidebar; }
.grid-main { grid-area: main; }
.grid-footer { grid-area: footer; }
```

## 17. What does `1fr` mean?

`fr` means a fraction of the grid's available flexible space. In `240px 1fr`, the browser accounts for the fixed column and gap, then gives the remaining flexible width to the `1fr` column. In `2fr 1fr`, the flexible space is divided into three shares: two for the first column and one for the second. Content minimum sizes can still affect a track's final size.

## 18. What does `repeat(3, 1fr)` mean?

It is a shorter way to write `1fr 1fr 1fr`. It creates three equal flexible columns. The gallery uses this for its desktop layout, so nine images form three rows of three images.

```css
.gallery {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}
```

## 19. How do responsive media queries work?

A media query applies a group of CSS rules only when its condition matches. `@media (max-width: 768px)` applies when the viewport is `768px` wide or narrower. The later rules override matching earlier rules according to the normal cascade.

```css
@media (max-width: 768px) {
    .cards-container {
        flex-direction: column;
    }

    .portfolio-layout {
        grid-template-columns: 1fr;
    }
}
```

In this project, the gallery changes to two columns at `1000px` and one column at `520px`. The card row, named areas, and portfolio adapt at `768px`. These widths are CSS viewport pixels, not a test for a particular phone model.

## 20. Why did we use Flexbox for navigation?

The logo and navigation need to share one horizontal row. Flexbox makes their spacing and vertical alignment straightforward with `justify-content`, `align-items`, and `gap`. The link list can wrap when there is not enough room.

## 21. Why did we use Grid for page structure?

The Grid Areas example needs both rows and columns: a full-width header, a sidebar beside the main area, and a full-width footer. Grid expresses that arrangement directly and lets the mobile layout change by redefining the columns and named areas.

## 22. Why do project cards use Flexbox internally?

The title, description, and action follow a single vertical direction. `flex-direction: column` describes that order clearly. `margin-top: auto` on `.project-action` consumes any spare space above the action, keeping it at the bottom of the card when spare height is available. The action uses native `<details>` and `<summary>` elements to reveal project notes without JavaScript.

## 23. How do equal-height cards work?

The desktop `.cards-container` is a single Flexbox row with cross-axis stretching. The tallest card's content establishes the row height, and the other cards stretch to match. Each `.card` is also a column-based flex container. Inside it, `.card-body` is another flex column with `flex: 1`, so the body fills the available space below the image. Its `.card-action` uses `margin-top: auto` to absorb the spare space above the action, which aligns the actions at the bottom. `flex: 1` shares width, not height, for the cards in the outer row.

```css
.cards-container {
    display: flex;
    align-items: stretch;
    gap: 24px;
}

.card {
    display: flex;
    flex-direction: column;
    flex: 1;
}

.card-body {
    display: flex;
    flex-direction: column;
    flex: 1;
}

.card-action {
    margin-top: auto;
}
```

On mobile, the cards become a column and may naturally have different content-based heights. They do not need an arbitrary fixed height to remain readable.

## 24. How does the gallery hover overlay work?

The gallery item uses `position: relative`, giving its absolutely positioned caption a local positioning reference. `overflow: hidden` clips both the caption and the slightly scaled image to the card's rounded boundary. The caption starts transparent, and `transition` animates its opacity when a user hovers the item.

```css
.gallery-item {
    position: relative;
    overflow: hidden;
}

.gallery-caption {
    position: absolute;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.gallery-item:hover .gallery-caption,
.gallery-item:focus .gallery-caption {
    opacity: 1;
}
```

The focus rules make the caption available to keyboard users. The actual stylesheet also keeps captions visible on devices without hover. `object-fit: cover` fills the image box while preserving the image's aspect ratio, cropping edges when needed instead of stretching the photo.

# Possible Live Coding Questions

These snippets are small changes to the existing CSS. Edit the original matching declaration or place an override after it. If a media query overrides the same property, change the rule for the viewport being demonstrated.

## Teacher: Make cards vertical.

**Answer:** Change the outer container's main direction to a column.

```css
.cards-container {
    flex-direction: column;
}
```

## Teacher: Center Flexbox items horizontally.

**Answer:** For a row-based container, use `justify-content: center`. The link list is a useful example because its links do not expand to fill all available width.

```css
.nav-links {
    display: flex;
    flex-direction: row;
    justify-content: center;
}
```

The effect is visible when the container has spare horizontal space. If its width is exactly its contents, temporarily give it a wider available area. For a column-based container, use `align-items: center` for horizontal centering instead. In the card row, `flex: 1` already consumes spare width, so centering may not visibly move those cards.

## Teacher: Change the gallery to four columns.

**Answer:** Change the repeat count in the desktop rule.

```css
.gallery {
    grid-template-columns: repeat(4, 1fr);
}
```

Nine images will create two full rows and one image in the third row. The existing media queries can still reduce the columns on smaller screens.

## Teacher: Increase the gap.

**Answer:** Increase `gap` on the relevant container, for example the gallery.

```css
.gallery {
    gap: 32px;
}
```

Use `.cards-container` instead if the teacher means the Flexbox cards. Gap creates space between items, while padding creates space inside the container's outer edges.

## Teacher: Move the sidebar under the main content on mobile.

**Answer:** Redefine the named Grid Areas inside the mobile media query. Also use one column and four rows.

```css
@media (max-width: 768px) {
    .grid-layout {
        grid-template-columns: 1fr;
        grid-template-rows: auto auto auto auto;
        grid-template-areas:
            "header"
            "main"
            "sidebar"
            "footer";
    }
}
```

The original mobile example puts the sidebar before the main area; this change reverses those two visual regions. Grid positioning does not change the HTML reading or keyboard order. If the new order should be permanent and includes interactive content, review the HTML order too. The portfolio's information sidebar already follows its projects in the one-column mobile layout.

## Teacher: Change Grid columns from 240px plus the rest to 300px plus the rest.

**Answer:** Change the fixed first column and leave the flexible column unchanged.

```css
.grid-layout {
    grid-template-columns: 300px 1fr;
}
```

The sidebar becomes wider, and the main area receives the remaining width after the sidebar and gap. Keep the one-column mobile override.

## Teacher: Center items vertically.

**Answer:** In a row-based Flexbox container, vertical alignment is controlled by `align-items`.

```css
.navbar {
    display: flex;
    flex-direction: row;
    align-items: center;
}
```

For a column-based Flexbox container, vertical alignment is along the main axis, so use `justify-content: center` instead. It only produces visible centering when there is spare height. An auto margin can absorb that space first, so account for `.card-action { margin-top: auto; }` when experimenting inside a card.

## Teacher: Make navigation links wrap.

**Answer:** Allow the link list's flex items to move onto another line.

```css
.nav-links {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
}
```

If the logo and the whole link list also need to move onto separate lines, add `flex-wrap: wrap` to the outer `.navbar` container.

## Teacher: Explain `grid-template-areas`.

**Answer:** It draws the layout as named cells. Each string is one row; matching repeated names span several cells. Children use `grid-area` to select their region.

```css
.grid-layout {
    display: grid;
    grid-template-columns: 240px 1fr;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
}

.grid-sidebar {
    grid-area: sidebar;
}
```

Here, the sidebar occupies the left cell of the middle row. The header and footer each occupy both columns. Renaming an area requires updating both the parent template and the child's matching `grid-area` value.

## Short Project Introduction to Practice

“My project is a personal developer portfolio built with HTML5 and CSS3. I used Flexbox for navigation, the card row, and the content inside cards. I used CSS Grid for the labelled page layout, the nine-image gallery, and the two-column portfolio. Media queries change these layouts for smaller screens. The page works without JavaScript, and all gallery images are stored locally.”
