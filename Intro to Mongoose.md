Date: Jun 4, 2022
Course: [[Web Development]] - [[Mongoose]]
- - -

## Questions

- Why do we need a schema? Will it make the database become SQL instead of noSQL? 
	- No, data is still flexible
	- eg: we can choose not to add name to document despite the schema
- Collection vs database?
	- A database contains a collection, a collection contains documents and the documents contain data.
	- Database > Collection > Document > Data 
- Schema vs Model: 
	- In mongoose, a schema represents the structure of a particular document, either completely or just a portion of the document.
	- Model defines a programming interface to interact with database (predefined methods such as CRUD)
	- Model is kinda like class implementing a Schema interface, and documents are instances of the Model class.
	-  A model is a representation of a database record as a nice object, with extra methods.

## Introduction

Mongoose is an Object Data Modeling (ODM) library for Node.js and MongoDB. It provides a higher-level, more expressive API for working with MongoDB, allowing developers to define models with schemas and apply custom methods to them.

With Mongoose, developers can define a schema for their data, which includes the fields, data types, and validation rules for their data. This makes it easier to work with complex data structures and ensures that the data stored in the database is consistent and valid.

##### Commands
- How to open and drop db in **MongoDB shell**:
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
```mongodb
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

```Mongodb
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
```mongodb
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

