# CSS Specificity

## Introduction

CSS specificity helps the browser decide which style to apply when more than one selector targets the same element. It is part of the CSS cascade, which also considers importance, cascade layers and source order.

## Basic Specificity Rules

- **ID selectors**, such as `#title`, have higher specificity than class selectors.
- **Class selectors**, such as `.title`, have higher specificity than element selectors.
- **Element selectors**, such as `p`, have lower specificity than classes and IDs.
- If two competing rules have equal specificity and the same cascade priority, the later rule normally wins.

## Example

```html
<p id="notice" class="message">Hello!</p>
```

```css
p { color: blue; }
.message { color: green; }
#notice { color: red; }
```

The text appears red because the ID selector has the highest specificity among these rules. Using too many IDs or `!important` declarations can make CSS harder to change later.

## Conclusion

Understanding specificity helps us fix style conflicts and write simpler, more maintainable CSS.

## References

- [MDN - CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_cascade/Specificity)
- [MDN - CSS Cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_cascade/Cascade)
