##### Topic: Read Data in Mongoose
Date: Jun 4, 2022
Course: [[Web Development]] - [[Mongoose]]
- - -

### Questions/Cues

### Notes
Returns an array of Fruit objects:
```JavaScript
Fruit.find(
	function(err, fruits) {
		if (err) {
			console.log(err);
		} else {
			cnsole.log(fruits);
		}
	}
);
```

Loop through the fruit objects to return each fruit name:
```JavaScript
fruits.forEach(function(fruit) {
	console.log(fruit.name);
})
```

We should close the connection to the database after opening it.
```JavaScipt
mongoose.connection.close();
```
### Summary

