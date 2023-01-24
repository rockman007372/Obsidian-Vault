##### Topic: Updating and Deleting Data with Mongoose
Date: Jun 4, 2022
Course:
- - -

### Questions/Cues

### Notes
- To update a document:
```JavaScript
Fruit.updateOne(
	{_id: ...},
	{name: "Peach"}, // add field "name" to this document
	function(err) {
		if (err) {
			console.log(err);
		} else {
			console.log("successful update");
		}
	}
);
```

- To delete a document:
```Node.js
Fruit.deleteOne(
	{name: "Peach"},
	function(err) {
		if (err) {
			console.log(err);
		} else {
			console.log("successful update");
		}
	}
);
```

- Delete many documents matching a particular conditions
```Node.js
Fruits.deleteMany({condition}, function(err){});
```

### Summary

