## MongoDB

### DBs

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
> 
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
```

### Read

```
findOne(filter, options)
find(filter, options)
```

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
deleteOne(filter, options)
deleteMany(filter, options)
```

## Filters

{field: value}
{field: {$gte: value}} greater value


#### Array queries

How to get an array element with a field that matchs a certain value?
