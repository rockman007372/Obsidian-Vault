2022-06-13 11:15
Tags: [[Web Development]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Introduction
HTML = Hyper Text Markup Language

An HTML element is defined by a start tag, some content, and an end tag.

An HTML elements can have attributes which give browsers extra info.

### Anatomy
1. **Opening tag and closing tag:** 
```HTML
<h1> title </h1>
```

2. **Self closing tag:**
```HTML
<br>
<img src="images/firefox-icon.png" alt="My test image">
<hr>
```
These are called empty elements (have no content in them) and they do not need a closing tag.

3. **HTML elements can have *attributes*:** 
```HTML
<hr size="3" noshade>
```
An attribute should always have the following:
1. A space between it and the element name (or the previous attribute, if the element already has one or more attributes).
2. The attribute name followed by an equal sign.
3. The attribute value wrapped by opening and closing quotation marks.

### List of HTML elements
https://www.w3schools.com/html/html_elements.asp

### Example of HTML codes
```HTML
<!DOCTYPE html> <!-- Necessary preamble -->
<html lang="en"> <!-- the root element, with English attribute -->
	<head> 
		<meta charset="utf-8" />
		<title>Hello!</title> 
	</head> 
	<body> 
		Hello, world! 
	</body> 
</html>
```

![[Pasted image 20220613114044.png]]

---

```HTML
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>HTML Elements</title>
    </head>
    <body>
        <!-- We can create headings using h1 through h6 as tags. -->
        <h1>A Large Heading</h1>
        <h2>A Smaller Heading</h2>
        <h6>The Smallest Heading</h6>

        <!-- The strong and i tags give us bold and italics respectively. -->
        A <strong>bold</strong> word and an <i>italicized</i> word!

        <!-- We can link to another page (such as cs50's page) using a element and href atribute. -->
        View the <a href="https://cs50.harvard.edu/">CS50 Website</a>!

        <!-- We used ul for an unordered list and ol for an ordered one. both ordered and unordered lists contain li, or list items. -->
        An unordered list:
        <ul>
            <li>foo</li>
            <li>bar</li>
            <li>baz</li>
        </ul>
        An ordered list:
        <ol>
            <li>foo</li>
            <li>bar</li>
            <li>baz</li>
        </ol>

        <!-- Images require a src attribute, which can be either the path to a file on your computer or the link to an image online. It also includes an alt attribute, which gives a description in case the image can't be loaded. -->
        An image:
        <img src="../../images/duck.jpeg" alt="Rubber Duck Picture">
        <!-- We can also see above that for some elements that don't contain other ones, closing tags are not necessary. -->

        <!-- Here, we use a br tag to add white space to the page. -->
        <br/> <br/>

        <!-- A few different tags are necessary to create a table. -->
        <table>
            <thead>
                <th>Ocean</th>
                <th>Average Depth</th>
                <th>Maximum Depth</th>
            </thead>
            <tbody>
                <tr>
                    <td>Pacific</td>
                    <td>4280 m</td>
                    <td>10911 m</td>
                </tr>
                <tr>
                    <td>Atlantic</td>
                    <td>3646 m</td>
                    <td>8486 m</td>
                </tr>
            </tbody>
        </table>
    </body>
<html>
```
![[Pasted image 20220613115025.png]]


Seel also [[Document Object Model]] to understand structure of HTML codes.




