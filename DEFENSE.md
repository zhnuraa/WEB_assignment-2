# Assignment 2 - Defense Notes

Nurassyl Zhumagul | IT-2501

## Main ideas

1. **Flexbox** arranges items in a row or a column. I used it for navigation and cards.
2. **CSS Grid** arranges items in rows and columns. I used it for the layout, gallery and portfolio.
3. **Difference:** Flexbox mainly controls one direction. Grid controls rows and columns together.
4. **Main axis:** the direction of the flex items. With `row`, it is horizontal on this page.
5. **Cross axis:** the direction across the main axis. With `row`, it is vertical.
6. **display: flex** makes the direct children of an element flex items.
7. **justify-content** controls space on the main axis. `space-between` puts the name and links at opposite ends of the navbar.
8. **align-items** controls the cross axis. `center` vertically centers the navbar items.
9. **flex-direction** sets the direction. I use `column` inside each card.
10. **gap** adds space between items. My card row has a 20px gap.
11. **flex: 1** lets items grow and shrink to share space. The three cards share the row width equally.
12. **display: grid** makes the direct children grid items.
13. **grid-template-columns** sets column sizes. `200px 1fr` means a 200px sidebar and a flexible main column.
14. **grid-template-rows** sets row sizes. My Grid Areas example uses `auto 1fr auto`. The content determines the height when no extra height is set.
15. **grid-template-areas** describes the layout with names. Each quoted line is a row.
16. **grid-area** puts a child in its named area, such as `grid-area: sidebar`.
17. **1fr** means one share of the available flexible space in a grid.
18. **repeat(3, 1fr)** creates three equal flexible columns. It is the same as `1fr 1fr 1fr`.
19. **Media query:** the rules inside `@media (max-width: 768px)` apply when the browser is 768px wide or smaller.
20. **Why Flexbox for navigation?** The name and links need to share one row with clear spacing and alignment.
21. **Why Grid for the page layout?** It needs a header and footer across two columns, with a sidebar beside the main content.
22. **Why Flexbox inside project cards?** The title, text and button go in a column. `margin-top: auto` on the button uses any spare space above it.
23. **Equal card heights:** the outer row uses `align-items: stretch`. Each card stretches to the height of the tallest card. The button's auto top margin aligns the buttons at the bottom. `flex: 1` shares width; stretching gives equal height.
24. **Gallery overlay:** the image box is `position: relative`. The caption is `position: absolute` at the bottom. Hover changes its opacity from 0 to 1. Keyboard focus also shows it, and captions stay visible on mobile.

## A few other properties in my CSS

- `box-sizing: border-box` includes padding and borders in the element's width.
- `object-fit: cover` fills the image box without stretching the photo. Some edges can be cropped.
- `min-width: 0` allows a flex card to shrink instead of being held wide by its image.
- `align-self: flex-start` keeps a button at its normal width inside a flex column.
- `overflow: hidden` keeps the gallery content inside its image box.
- `rgba(0, 0, 0, 0.7)` is black with 70% opacity. The caption text stays white.
- `transition: opacity 0.2s` makes the caption appear over 0.2 seconds.
- `tabindex="0"` lets a gallery figure receive keyboard focus.
- The blue buttons are `<a>` links because they move to another part of the page. They work without JavaScript.

## Possible Live Coding Questions

### Make cards vertical.

```css
.cards-container {
    flex-direction: column;
}
```

### Center Flexbox items horizontally.

For a row, use `justify-content`. It needs some free space to have a visible effect.

```css
.nav-links {
    justify-content: center;
}
```

For a column, horizontal alignment uses `align-items` instead.

### Change the gallery to four columns.

```css
.gallery {
    grid-template-columns: repeat(4, 1fr);
}
```

### Increase the gap.

```css
.cards-container {
    gap: 30px;
}
```

### Move the sidebar under main content on mobile.

Change the existing mobile rule:

```css
.grid-container {
    grid-template-areas:
        "header"
        "main"
        "sidebar"
        "footer";
}
```

The mobile rule already sets one column. This changes the visual order; it does not change the HTML reading order.

### Change the sidebar width to 300px.

```css
.grid-container {
    grid-template-columns: 300px 1fr;
}
```

My current desktop sidebar is 200px. The same change would work if it started at 240px.

### Center items vertically.

For a row:

```css
.navbar {
    align-items: center;
}
```

For a column, vertical alignment uses `justify-content` and needs spare height.

### Make navigation links wrap.

```css
.nav-links {
    flex-wrap: wrap;
}
```

### Explain grid-template-areas.

```css
.grid-container {
    grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
}

.grid-sidebar {
    grid-area: sidebar;
}
```

The header and footer cover both columns. The sidebar is on the left of the main content. The names on the parent and children must match.

## Short introduction to practice

My first assignment used basic HTML and CSS. In this assignment, I learned Flexbox and Grid. I used Flexbox for the navigation and cards. I used Grid for the page layout, gallery and portfolio. One media query changes the layout on small screens.
