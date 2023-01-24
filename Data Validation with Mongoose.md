##### Topic: Data Validation with Mongoose
Date: Jun 4, 2022
Course: [[Web Development]] - [[Mongoose]]
- - -

### Questions/Cues

### Notes
Validation of data entry = checks if data registered into database is valid.

```Node.js
const fruitSchema = new mongoose.Schema({
	name: {
		type: String,
		required: [true, "why no fruit name"] // require name
	},
	rating: {
		type: Number,
		min: 1, // min rating is 1
		max: 10
	},
	review: String
});

const fruit = new Fruit({
	// name: "Apple" -> fruit with no name
	rating: 34, // -> out of bound
	review: "ass"
});
```

### Summary

