---
tags:
  - noSQL
aliases: 
date: 2022-07-24 Sunday
---
- MongoDB is a NoSQL **document-oriented** database system. 
- Handle unstructured or semi-structured data.
- Data is stored as documents, which are similar to [[JSON]] objects. Each document can have its own unique schema, and can contain nested data structures, arrays, and other complex data types. 

## CRUD Commands

CRUD = CREATE, READ, UPDATE, DELETE

**CREATE**
- db -> show which dbase u are in
- db.collection.insertOne( JavaScript object )
```mongodb
db.users.insertOne(
	{
		name: "Nate",
		age: 26,
		status: "pending"
	}
)
```
- db.collection.insertMany( ... )
- collections = columns in sql database

**READ**
- db.collection.find() -> find all data in collection
- db.collection.find(query, projection) -> find specific queries with conditions
```mongodb
db.products.find({name: "Pencil"})

db.products.find(
	{
		price: {$gt: 1} // greater than 1
	}
)
```
- projection toggles visibility of fields
```SQL
dp.products.find({id: 1}, {name: 1, id: 0}) 
-> show name field but not id
```

**UPDATE**

```SQL
db.products.updateOne(
	{id: 1}, 
	{$set: {stock: 32}}
)
db.products.updateOne({id: 2}, {$set: {stock: 12}})
```

**DELETE**

```SQL
db.collection.deleteOne({id: 2})
```

**Relationship**

```SQL
db.products.insert(
	{
		id: 3,
		price: 1.30,
		stock: 43,
		reviews: [ // Array of reviews
			{
				authorName: "Sally"
				rating: 5
				review: "shits good"
			},
			{
				authorName: "John"
				rating: 1
				review: "shit ass"
			}
		]
	}
)
```

Another way to link many data together using array:

```SQL
{
	id: 1,
	name: "Vibrator"
}

{
	id: 2,
	name: "Dildo"
}

{
	orderNumber: 3243,
	productsOrdered: [1, 2]
}
```


