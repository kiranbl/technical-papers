# CSS Flexbox and Grid

## Introduction

Flexbox and Grid are CSS layout systems. **Flexbox** is useful for arranging items in a row or column, while **Grid** is useful for arranging items in rows and columns together. Both help build responsive websites.

## 1. Flexbox

Flexbox uses a **main axis** and a **cross axis** .

### Flexbox Container Properties

| Property | Purpose |
|---|---|
| `display: flex` | Enables Flexbox. |
| `flex-direction` | Sets row or column direction. |
| `justify-content` | Aligns items along the main axis. |
| `align-items` | Aligns items along the cross axis. |
| `flex-wrap` | Allows items to wrap to another line. |
| `gap` | Adds space between items. |

### Flexbox Item Properties

| Property | Purpose |
|---|---|
| `flex-grow` | Controls how an item grows into free space. |
| `flex-shrink` | Controls how an item shrinks. |
| `flex-basis` | Sets the starting size of an item. |
| `flex` | Shorthand for grow, shrink, and basis. |
| `align-self` | Aligns one item on the cross axis. |
| `order` | Changes visual order, not reading order. |

### Example

```css
.nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
}
```

This arranges navigation links in a row with space between them.

## 2. CSS Grid

Grid helps create layouts with multiple **rows and columns**, such as galleries and page sections.

### Grid Container Properties

| Property | Purpose |
|---|---|
| `display: grid` | Enables Grid. |
| `grid-template-columns` | Defines columns and their sizes. |
| `grid-template-rows` | Defines rows and their sizes. |
| `grid-template-areas` | Names regions of a layout. |
| `gap` | Adds space between rows and columns. |
| `justify-items` | Aligns items horizontally inside their areas. |
| `align-items` | Aligns items vertically inside their areas. |

### Grid Item Properties

| Property | Purpose |
|---|---|
| `grid-column` | Sets the columns an item occupies. |
| `grid-row` | Sets the rows an item occupies. |
| `grid-area` | Places an item in a named area or grid position. |
| `justify-self` | Aligns one item horizontally. |
| `align-self` | Aligns one item vertically. |

### Useful Grid Values

- **`fr`:** Divides available space into fractions.
- **`repeat()`:** Repeats column or row sizes.
- **`minmax()`:** Sets minimum and maximum track sizes.
- **`auto-fit`:** Fits repeated tracks and collapses unused ones.

### Example

```css
.gallery {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 15px;
}

@media (max-width: 600px) {
    .gallery {
        grid-template-columns: 1fr;
    }
}
```

The gallery has three columns on wider screens and one column on small screens.

## Flexbox vs. Grid

| Flexbox | Grid |
|---|---|
| Best for a row or column. | Best for rows and columns together. |
| Useful for navigation and buttons. | Useful for galleries and page layouts. |

## Conclusion

Flexbox is helpful for aligning items in one direction, while Grid gives more control over rows and columns. We can use both in the same website to make layouts easier to manage.

## References

- [MDN - Basic Concepts of Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox)
- [MDN - Flexbox Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout)
- [MDN - Basic Concepts of Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Basic_concepts_of_grid_layout)
- [MDN - Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout)
- [MDN - Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries)
