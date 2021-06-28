## MongoDB

### DBs general shit

```
> show dbs


TestDb  0.000GB
admin   0.000GB
config  0.000GB
local   0.000GB
shop    0.000GB
> use shop
switched to db shop
> db.dropDatabase()
{ "dropped" : "shop", "ok" : 1 }
> db.createCollection('test')
{ "ok" : 1 }
> db.test.drop()
true

```
### Collections

```
db.createCollection('collectionName')
db.collectionName.drop()
```


### CRUD Operations

### Create

```insertOne(doc, options)
insertMany([doc1, doc2...], options)
insert(doc, options)
```
*insert* is less interresting becauses it doesn't return the insert document IDs.

option {ordered: false} keeps writing elements even if their ID is not unique. It doesn't replace the element with matching IDs with their new content.

#### writeconcern

*writeconcern* is used to aknowledge success of document inserction.
We can add {j: true} option so we journal the oprations to make them quicker but it will be slower to insert them.
You can have a writetimeout option set up in ms. In case the insertion is too long you will be able to instantly retry instead of waiting for a long operation. This is good if you have a sometime shaky connection but with good speed.



### Read

```
findOne(filter, options)
find(filter, options)
```

db.movies.find({genre: "Drama"})
if genres is an array it will look for every document with a genres array containing the string "Drama"
if we do:
db.movies.find({genre: ["Drama"]})

#### Projections

db.movies.find({}, {name: 1})
### Update

```
updateOne(filter, data, optionss)
updateMany(filter, data, options)
replaceOne(filter, data, options)
```

```
updateOne({_id: 1}, { $set: {
### Delete

```
```
deleteOne(filter, options)
deleteMany(filter, options)

```

## Filters

{field: value}
{field: {$gte: value}} greater value

### Document validation


```
db.createCollection('posts', {
	validator: {
		$jsonSchema: {
			bsonType: 'object',
			required: ['title', 'text', 'creator', 'comments'],
			properties: {
				title: {
					bsonType: 'string'
				},
				text: {
					bsonType: 'string'
				}
				creatorId: {
					bsonType: 'string'
				}
				comments: {
					bsonType: 'array',
					items: {
						bsonType: 'object',
						required: ['text', 'author'],
						properties: {
							text: {
								bsonType: 'string',
								description: 'must be a string'
							},
							authorId: {
								bsonType: 'objectId'
							}
						}
					}
				}
			}
		}
	}
});
```

**Update the validator schema:**

### Filters

Operators:

{$in: [1, 2, 3]}

coll: 
### MongoImport

### Indexes
```
db.products.createIndex({price: 1});
db.products.find(‘)
```

Moongose *unique* creates an unique index.
[Unique in mongoose](https://masteringjs.io/tutorials/mongoose/unique)

### Time to live



### Agregations

```
db.persons.aggregate([
    { $match: { gender: 'female' } },
    { $group: { _id: { state: "$location.state" }, totalPersons: { $sum: 1 } } },
    { $sort: { totalPersons: -1 } }
]).pretty();
```

https://docs.mongodb.com/manual/reference/aggregation-variables/#system-variables

*WTF IS *location.state*
```
CURRENT
References the start of the field path being processed in the aggregation pipeline stage. Unless documented otherwise, all stages start with CURRENT the same as ROOT.

CURRENT is modifiable. However, since $<field> is equivalent to $$CURRENT.<field>, rebinding CURRENT changes the meaning of $ accesses.

```

### Authorization and Roles Access

https://docs.mongodb.com/manual/tutorial/enable-authentication/


### Caping

```
db.dbName.createCollection('collectionName', {capped: true, size: 10000, limit: 3})
```

### Transactions

#### Session

```javascript
const s = db.getMongo().startSession()
s.startTransaction()
const postsCol = s.getDatabase('blog').posts
const usersCol = s.getDatabase('users').users
postCol.deleteOne({_id: 1});
s.commitTransaction()
```
or you can abord the transaction ```s.abortTransaction()```

Secure operations on documents by creating dependant documents. Operation won't be 
#### Questions?

WTF is *db.collection.initializeOrderedBulkOp()*?
