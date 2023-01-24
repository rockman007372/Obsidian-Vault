##### Topic: Basic CSS types
Date: Jun 4, 2022
Course:
- - -

### Questions/Cues

### Notes
Just a style language used to change the styles of markup languages (HTML).

*In-line CSS*: Have to add into element similar to attribute
```HTML
<body style="background-color: blue">
	...
</body>
```
- https://colorhunt.co/ to find good colour pallettes.
- Can google `CSS colours` for more details on when to use English and when to use Hash Code.

*Internal CSS:* We add the style like some sort of inner function/method
```HTML
<style>
	body {
		background-color: blue;
	}
</style>

<body>
	...
</body>
```

All browers have some preinstalled default CSS styles. 
- Eg: Border is already styled, cannot modify in index.html normally
- We can overwrite Border style by modifying its default styles
```HTML
<style>
	hr {
	    border-style: none; 
	    border-dotted-style: dotted;
	    // this is required to overwrite default style
	    background-color: white;
	    height: 2px;
	}
</style>
```

Internal CSS styles only works for a local HTML file. To apply it to all other HTML files, we can use *External CSS.*
- Create `css/style.css` inside your work folder
- Add link to style.css:
```HTML
<link rel="stylesheet" href="css/styles.css">
```

### Summary

