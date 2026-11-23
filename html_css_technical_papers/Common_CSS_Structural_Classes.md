# Common CSS Structural Classes

## Introduction

Structural classes are class names that developers use to organize the layout of a web page. Examples include `.container`, `.header`, `.navbar`, `.sidebar` and `.footer`. These are naming conventions, not special classes built into CSS. We define their styles ourselves.

## Common Examples

- **`.container`:** Keeps content within a readable width.
- **`.header`:** Holds the top section of a page.
- **`.navbar`:** Organizes navigation links.
- **`.sidebar`:** Holds secondary content beside the main section.
- **`.footer`:** Styles the bottom section of a page.

## Example

```html
<div class="container">
    <header class="header">My Website</header>
    <main class="content">Welcome!</main>
    <footer class="footer">Contact us</footer>
</div>
```

```css
.container {
    max-width: 1000px;
    margin: 0 auto;
}

.header, .footer {
    padding: 16px;
    background: lightgray;
}
```

The class names help us understand which part of the page we are styling. Semantic HTML elements such as `<header>`, `<main>` and `<footer>` also describe the meaning of each section.

## Conclusion

Clear structural class names make layouts easier to read, reuse and maintain as a website grows.

## References

- [MDN - CSS Class Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors)
- [MDN - HTML class Attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class)
