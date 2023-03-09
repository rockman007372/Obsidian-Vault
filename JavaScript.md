Topic: Intro to JavaScript
Date: Jun 3, 2022
Course: [[Web Development]]
- - -

## Introduction to JavaScipt

- JavaScript is a programming language that is commonly used to create interactive and dynamic web pages. 
- JavaScript code is executed by web browsers, and it can manipulate the content and behavior of web pages, interact with web servers to retrieve and send data, and provide dynamic functionality to web applications. 
- It is a versatile language that is used not only for web development but also for server-side scripting, desktop application development, game development, and other programming tasks.

## Characteristics

- Allows website to implement functionalities and behaviours. Gives instructions to HTML elements.
- Java vs JavaScipt: No relationship
- Javascript is an *interpreted* language (Translated and run line by line).

## Example Code

```javascript
alert("Hello World")

var myName = "nice"; // no need to define type

var yourName = prompt("Your name?"); 

myName.length; 

myName.slice(0, 5) // string between 0 && 4

```

### How to add JavaScript to HTML

Use the `<script>` element:

```HTML
<!DOCTYPE html> 
<html lang="en"> 
	<head> 
		<meta charset="utf-8" />
		<title>My Website</title>
		<link rel="stylesheet" href="style.css"> 
	</head> 
	<body> 
		<h1>Hello, world!</h1>
		
		<script> src="index.js" charset="urf-8"</script>
	</body> 
</html>
```

### How to modify HTML Elements with JavaScript

Select HTML elements with JavaScript: 

```JavaScript
// In command console:
document.firstChild;

document.getElementsByTagName("li") // return an array of elements with tag name <li></li> [foo, bar, baz]

// single element selector, return the first element found
document.getElementById("title").innerHTML = "fuck you";

document.querySelector("h1"); // get element

document.querySelector("#title"); // get id

document.querySelector(".btn"); // get class

document.querySelector("#list a") // combine selectors, get link inside the list with id = list

documnet.querySelectorAll(...); // array of all satisfied elements
```

Manipulate HTML elements and change styles with JavaScript:

```JavaScript
document.getElementsByTagName("li")[1].styles.colour = "red";

document.querySelector("h1").styles.width = "30";

// values of properties must be stated in type String
```

Modify CSS class in HTML elements:

```JavaScript
document.querySelector("button").classList.add("invisible");

document.querySelector("button").classList.remove("invisible");

document.querySelector("button").classList.toggle("invisible");
```

Text manipulation:

```Java
document.querySelector("h1").innerHTML("<em>Fuck</em>"); // not just change text but also html element
```

Manipulate HTML elements attributes:

```JavaScript
document.querySelector("h1").attributes;

document.querySelector("h1").getAttribute("href");

document.querySelector("h1").setAttribute("href", "http://google.com");
```

