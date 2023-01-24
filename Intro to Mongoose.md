
Topic: Intro to Mongoose
Date: Jun 4, 2022
Course: [[Web Development]] - [[Mongoose]]
- - -

### Questions/Cues
- Why do we need a schema? Will it make the database become SQL instead of noSQL? 
	- No, data is still flexible
	- eg: we can choose not to add name to document despite the schema
- Colletion vs database?
	- A database contains a collection, a collection contains documents and the documents contain data.
	- Database > Collection > Document > Data 
- Schema vs Model: 
	- In mongoose, a schema represents the structure of a particular document, either completely or just a portion of the document.
	- Model defines a programming interface to interact with database (predefined methods such as CRUD)
	- Model is kinda like class created from a Schema, and documents are instaces of the Model class
	-  A model is a representation of a database record as a nice object, with extra methods.

### Notes
##### Introduction
- Mongoose = ODM (Object Development Mapper), allow Node.js JavaScript language to interact with MongoDB language of documents and collections.
- Vastly shorter than MongoDB Drivers

##### Commands
- How to open and drop db in MongoDB shell:
```MongoDB
> show dbs
> use fruitsDB
> db.dropDatabase()
```

- Install Mongoose package: 
```
// in DB 
>npm i moongoose
```

- How to insert documents into database: 
```Node.js
// use package Mongoose
const mongoose = require('mongoose');

// connect Node.js to database
mongoose.connect(
	"mongodb://localhost:27017/fruitsDB"), 
	{ useNewUrlParser: true }
);

// Create a blueprint/structure of the document
const fruitSchema = new mongoose.Schema(
	{
		name: String,
		rating: Number,
		review: String
	}
);

// Create a new collection called Fruits
// Collection name MUST BE SINGULAR
const Fruit = mongoose.model("Fruit", fruitSchema);

// Create a document
const fruit = new Fruit({
	name: "Apple",
	rating: 7,
	review: "Pretty good"
});

fruit.save(); // save apple into Fruit collection inside FruitDB

```

```Node.js
const personSchema = new mongoose.Schema({
	name: String,
	age: Number
});

const Person = mongoose.model("Person". personSchema);

const person = new Person({
	name: "John"
	age: 37
});

person.save();
```

- The following Schema Types are permitted:
	-   Array
	-   Boolean
	-   Buffer
	-   Date
	-   Mixed (A generic / flexible data type)
	-   Number
	-   ObjectId
	-   String

- Add data in bulk:
```Node.js
const kiwi = new Fruit({});
const orange = new Fruit({});
const banana = new Fruit({});

Fruit.insertMany(
	[kiwi, orange, banana], 
	function(err) {
		if (err) {
			console.log(err);
		} else {
			console.log("Success");
		}
	}
)
```

### Summary
Highlight <mark style="background: #ADCCFFA6;">what’s important!</mark> 

