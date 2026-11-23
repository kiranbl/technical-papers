# Responsive CSS Media Queries

## Introduction

Responsive design helps websites work well on mobile phones, tablets and computers. CSS media queries apply different styles when conditions such as viewport width are met. This allows a layout to adjust without creating separate web pages for every screen size.

## How Media Queries Work

A media query begins with `@media` and includes a condition. For example, `max-width: 600px` targets viewports that are 600 pixels wide or less. We can use it to change spacing, text sizes, or the number of columns.

## Example

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

@media (max-width: 600px) {
    .container {
        grid-template-columns: 1fr;
    }
}
```

On wider screens, this container has two columns. On narrower screens, it changes to one column so the content has more room. The `<meta name="viewport">` tag also helps mobile browsers use the intended viewport width.

## Conclusion

Media queries help create flexible layouts that are easier to use across different devices.

## References

- [MDN - Using Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- [MDN - Responsive Design](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design)
