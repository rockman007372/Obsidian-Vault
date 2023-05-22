#### Add JavaScript to HTML

Add the `<script>` element at the end of the body element.

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
		
		<script> src="index.js" charset="urf-8"</script> -- script added
	</body> 
</html>
```

#### Modify HTML Elements

Select HTML elements:

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

Manipulate HTML elements and change styles:

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
