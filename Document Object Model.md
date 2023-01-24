##### Topic: Document Object Model
Date: Jun 4, 2022
Course:
- - -

### Questions/Cues

### Notes
##### How to add JavaScript to website
- Use the `<script>` elemente
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

##### Introduction
- Visualize HTML elements in a tree-like structure:
![[Pasted image 20220613113812.png|500]]

- Select HTML elements with JavaScript: 
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

- Manipulate HTML elements and change styles with JavaScript:
```JavaScript
document.getElementsByTagName("li")[1].styles.colour = "red";

document.querySelector("h1").styles.width = "30";

// values of properties must be stated in type String
```

- Modify CSS class in HTML elements:
```JavaScript
document.querySelector("button").classList.add("invisible");

document.querySelector("button").classList.remove("invisible");

document.querySelector("button").classList.toggle("invisible");
```

- Text manipulation:

```Java
document.querySelector("h1").innerHTML("<em>Fuck</em>"); // not just change text but also html element
```

- Manipulate HTML elements attributes:
```JavaScript
document.querySelector("h1").attributes;

document.querySelector("h1").getAttribute("href");

document.querySelector("h1").setAttribute("href", "http://google.com");
```

