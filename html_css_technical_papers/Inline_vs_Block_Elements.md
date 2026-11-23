# Inline and Block Elements

## Introduction

HTML elements have different display behaviors. Two common types are block and inline elements. Knowing the difference helps us decide how content should appear on a page. CSS can also change the default behavior of an element.

## Block Elements

Block elements usually begin on a new line and stretch across the available width of their container. Common examples include `<div>`, `<p>` and `<h1>`.

## Inline Elements

Inline elements usually appear within the same line as nearby text. They take only the space needed for their content. Common examples include `<span>`, `<a>` and `<strong>`.

## Example

```html
<p>This paragraph starts on a new line.</p>
<span>Hello</span>
<span>World</span>
```

The paragraph is displayed as a separate block. The two spans normally appear next to each other. We can use CSS such as `display: block`, `display: inline`, or `display: inline-block` to change how an element behaves.

## Conclusion

Block elements are useful for page sections, while inline elements are useful for short pieces of text or links inside a line.

## References

- [MDN - Block and Inline Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_display/Block_and_inline_layout_in_normal_flow)
- [MDN - display](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
