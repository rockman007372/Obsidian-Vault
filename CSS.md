Date: Jun 4, 2022
Course: [[Web Development]]
- - -

CSS is a style language used to change the styles of markup languages (HTML). There are 3 ways to apply CSS to HTML elements.

## In-line CSS

Inline CSS is applied directly to individual HTML elements using the "style" attribute.

```HTML
<body style="background-color: blue">
	...
</body>
```
- https://colorhunt.co/ to find good colour pallettes.
- Can google `CSS colours` for more details on when to use English and when to use Hash Code.

## Internal CSS 

Internal CSS is defined within the `<head>` section of an HTML document using the `<style>` tag. It applies to all the elements on the page that match the selectors specified in the style rules.

```HTML
<head>
  <style>
    p {
      color: red;
    }
  </style>
</head>

<body>
  <p>This is a red paragraph</p>
</body>
```

Internal CSS can be more efficient than inline CSS because it separates the style rules from the HTML code, making it easier to update and maintain the styles of multiple elements at once.

## External CSS Stylesheet

Internal CSS styles only works for a local HTML file. To apply it to all other HTML files, we can use **External CSS**.

External CSS is defined in a separate .css file, which is linked to the HTML document using the `<link>` tag in the `<head>` section. External CSS allows developers to keep the style rules separate from the HTML code and reuse them across multiple pages.

```HTML
<link rel="stylesheet" href="css/styles.css">
```

Where `style.css` file contains:

```css
.red-paragraph {
  color: red;
}
```

External CSS is generally considered the best practice for applying styles to HTML documents because it promotes separation of concerns and makes the code easier to maintain and scale.

### Summary

