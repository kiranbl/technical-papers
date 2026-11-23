# CSS Box Model

## Introduction

The CSS box model explains how browsers calculate the space used by an HTML element. Every visible element is treated like a rectangular box. Understanding this model helps us control spacing and prevent layout problems when building web pages.

## Parts of the Box Model

- **Content:** The text, image, or other content inside the element.
- **Padding:** The space between the content and its border.
- **Border:** The line surrounding the padding and content.
- **Margin:** The space outside the border that separates elements.

## Example

```css
.card {
    width: 300px;
    padding: 20px;
    border: 2px solid black;
    margin: 10px;
    box-sizing: border-box;
}
```

Here, the card has a declared width of 300 pixels. Because it uses `border-box`, the padding and border are included inside that width. The margin stays outside it. Without `border-box`, the padding and border would increase the total width.

## Conclusion

The box model makes spacing easier to understand. It is useful when designing cards, forms, navigation bars, and other page elements.

## References

- [MDN - CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_box_model)
- [MDN - box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)
