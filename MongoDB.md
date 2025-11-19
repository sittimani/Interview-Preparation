# MongoDB Quick Reference

A beginner-friendly MongoDB cheat sheet with core concepts, simple explanations, and examples.

---

## 1. What is MongoDB?

MongoDB is a **NoSQL, document-based database** that stores data in **JSON-like documents** called **BSON**.

* Flexible schema
* Easy to scale
* Great for modern web apps

---

## 2. Database & Collection

* **Database** → A container for collections.
* **Collection** → A container for documents.
* **Document** → JSON-like data object.

---

## 3. Basic Commands

### Create / Use Database

```js
use myDatabase
```

### Show Databases

```js
show dbs
```

### Show Collections

```js
show collections
```

---

## 4. Insert Documents

### Insert One

```js
db.users.insertOne({ name: "Mani", age: 25 })
```

### Insert Many

```js
db.users.insertMany([
  { name: "Arun", age: 30 },
  { name: "Kumar", age: 28 }
])
```

---

## 5. Find Documents

### Find All

```js
db.users.find()
```

### Find with Filter

```js
db.users.find({ age: 25 })
```

### Find One

```js
db.users.findOne({ name: "Mani" })
```

### Find by ID

```js
db.users.findOne({ _id: ObjectId("64c1f3d8912af1a9c1e12345") })
```

---

## 6. Update Documents

### Update One

```js
db.users.updateOne(
  { name: "Mani" },
  { $set: { age: 26 } }
)
```

### Update Many

```js
db.users.updateMany(
  { age: { $lt: 20 } },
  { $set: { status: "minor" } }
)
```

---

## 7. Delete Documents

### Delete One

```js
db.users.deleteOne({ name: "Mani" })
```

### Delete Many

```js
db.users.deleteMany({ age: { $gt: 50 } })
```

---

## 8. Important Operators

### Comparison

```js
$eq, $ne, $gt, $lt, $gte, $lte
```

Example:

```js
db.users.find({ age: { $gt: 25 } })
```

### Logical

```js
$and, $or, $not, $nor
```

Example:

```js
db.users.find({
  $or: [ { age: 25 }, { name: "Kumar" } ]
})
```

### In / Not In

```js
db.users.find({ age: { $in: [25, 30] } })
```

---

## 9. Sorting & Limiting

### Sort

```js
db.users.find().sort({ age: 1 })  // ascending
```

### Limit

```js
db.users.find().limit(5)
```

---

## 10. Aggregation (Basic)

Aggregation is used for data processing like filtering, grouping, sorting, projecting, etc.

### Common Aggregation Stages

#### `$match` – Filter documents

```js
{ $match: { age: { $gt: 25 } } }
```

#### `$group` – Group and aggregate

```js
{ $group: { _id: "$age", total: { $sum: 1 } } }
```

#### `$project` – Select specific fields

```js
{ $project: { name: 1, age: 1, _id: 0 } }
```

#### `$sort` – Sort results

```js
{ $sort: { age: -1 } }
```

#### `$limit` – Limit results

```js
{ $limit: 5 }
```

#### `$skip` – Skip the first N docs

```js
{ $skip: 10 }
```

#### `$lookup` – Join two collections

```js
{
  $lookup: {
    from: "orders",
    localField: "_id",
    foreignField: "userId",
    as: "orders"
  }
}
```

#### `$unwind` – Break array into individual documents

```js
{ $unwind: "$orders" }
```

#### `$count` – Count docs

```js
{ $count: "totalUsers" }
```

### Example Full Pipeline

```js
db.users.aggregate([
  { $match: { age: { $gt: 25 } } },
  { $project: { name: 1, age: 1 } },
  { $sort: { age: -1 } },
  { $limit: 3 }
])
```

---

## 11. Indexes

### Create Index

```js
db.users.createIndex({ name: 1 })
```

### Show Indexes

```js
db.users.getIndexes()
```

---

## 12. Drop (Delete)

### Drop Collection

```js
db.users.drop()
```

### Drop Database

```js
db.dropDatabase()
```
