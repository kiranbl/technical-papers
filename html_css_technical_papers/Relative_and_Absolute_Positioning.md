# Relative and Absolute Positioning in CSS

## Introduction

CSS positioning controls where an element appears on the page. Two important values are `relative` and `absolute`. They are often used together to place items such as labels, icons and badges inside a card.

## Relative Positioning

An element with `position: relative` stays in the normal page layout. Properties such as `top` and `left` move its visual position, but its original space remains reserved.

## Absolute Positioning

An element with `position: absolute` is removed from the normal layout. It is positioned relative to its nearest ancestor that establishes a positioning containing block, often an ancestor with `position: relative`.

## Example

```html
<div class="card">
    Product
    <span class="badge">New</span>
</div>
```

```css
.card {
    position: relative;
    padding: 30px;
}

.badge {
    position: absolute;
    top: 5px;
    right: 5px;
}
```

The badge appears near the top-right corner of the card. Setting `position: relative` on the card gives the absolutely positioned badge a useful reference point.

## Conclusion

Relative positioning makes small adjustments, while absolute positioning helps place elements at specific locations inside a container.

## References

- [MDN - position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- [MDN - CSS Positioned Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_positioned_layout)
