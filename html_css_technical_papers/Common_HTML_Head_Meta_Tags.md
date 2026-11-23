# Common HTML Head Meta Tags

## Introduction

The HTML `<head>` element contains information about a web page that is mainly used by browsers, search engines and other services. Meta tags help describe the page and configure how it should be displayed. They do not normally appear as visible page content.

## Common Tags

- **`charset`:** Sets the character encoding, usually UTF-8.
- **`viewport`:** Helps control page sizing on mobile devices.
- **`description`:** Gives a short summary of the page.
- **`title`:** Names the browser tab. It is an HTML element, not a `<meta>` tag.

## Example

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Learn HTML and CSS basics">
    <title>HTML and CSS Guide</title>
</head>
```

The viewport tag is especially important when creating responsive layouts. The description may be used by search engines to summarize the page, although its display is not guaranteed. A clear title helps users identify a page in their browser tabs.

## Conclusion

Good head metadata helps browsers understand the page and improves the experience across devices.

## References

- [MDN - meta Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta)
- [MDN - head Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/head)
