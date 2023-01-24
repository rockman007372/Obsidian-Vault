##### Topic: Establish Relationship and Embed Document in Mongoose
Date: Jun 4, 2022
Course: [[Web Development]] - [[Mongoose]]
- - -

### Questions/Cues

### Notes
Establish relationship between documents (tables).

```JavaScript
const personSchema = new mongoose.Schema({
	name: String,
	age: Number,
	favouriteFruit: fruitSchema
});

const Person = mongoose.model("Person", personSchema);

const pineapple = new Fruit({/*...*/});

const Vienne = new Person({
	name: "Vienne",
	age: 21,
	favouriteFruit: pineapple
});
```

- Update current person with a new fruit:
```JavaSCript
// assuming John is already in the DB without a favourite fruit
Person.updateOne(
	{Name: "John"},
	{favouriteFruit: pineapple},
	function(err) {}
);
```

### Summary

