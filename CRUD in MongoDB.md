Topic: MongoDB
Date: Jun 3, 2022
Course: [[Web Development]] - [[Introduction to Databases]]
- - -

### Questions/Cues

### Notes
##### Introduction
MongoDB is a NonSQL database.

##### Commands in MongoDB
**CREATE**
- db -> show which dbase u are in
- db.collection.insertOne( JavaScript object )
```SQL
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

---
**READ**
- db.collection.find() -> find all data in collection
- db.collection.find(query, projection) -> find specific queries with conditions
```SQL
db.products.find({name: "Pencil"})

db.products.find(
	{
		price: {$gt: 1} # greater than 1
	}
)
```
- projection toggles visibility of fields
```SQL
dp.products.find({id: 1}, {name: 1, id: 0}) 
-> show name field but not id
```

---
**UPDATE**

```SQL
db.products.updateOne(
	{id: 1}, 
	{$set: {stock: 32}}
)
db.products.updateOne({id: 2}, {$set: {stock: 12}})
```

---
**DELETE**

```SQL
db.collection.deleteOne({id: 2})
```

---
**Relationship**

```SQL
db.products.insert(
	{
		id: 3,
		price: 1.30,
		stock: 43,
		reviews: [
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

- Another way to link many data together using array:
```SQL
{
	id: 1,
	name: "Pen"
}

{
	id: 2,
	name: "Dildo"
}

{
	orderNumber: 3243,
	productOrdered: [1, 2]
}
```

### Summary
