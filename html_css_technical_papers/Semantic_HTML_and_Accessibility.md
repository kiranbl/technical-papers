# Semantic HTML and Accessibility

## Introduction

Semantic HTML means using elements that describe the purpose of the content. For example, `<nav>` is used for navigation and `<main>` for the main content. Accessibility means designing web pages so more people, including those using assistive technologies, can use them.

## Common Semantic Elements

- **`<header>`:** Introductory content for a page or section.
- **`<nav>`:** A group of navigation links.
- **`<main>`:** The main content of the document.
- **`<footer>`:** Footer information for a page or section.
- **`<button>`:** An interactive control that can be used with a keyboard.

## Example

```html
<header><h1>My Website</h1></header>
<nav><a href="/about">About</a></nav>
<main>
    <h2>Welcome</h2>
    <img src="book.jpg" alt="A book on a desk">
    <button type="button">Read more</button>
</main>
```

The heading gives the page a clear structure. The image has alternative text for users who cannot see it. The button is a real HTML button instead of a clickable `<div>`, making keyboard use easier.

## Conclusion

Semantic HTML and accessibility make websites easier to understand, navigate and use for a wider range of people.

## References

- [MDN - HTML Elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements)
- [MDN - Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)
