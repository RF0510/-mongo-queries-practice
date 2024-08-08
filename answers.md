# MongoDB CLI

## Getting Started

The prompts below each ask for you to write the query in MongoDB for performing
some action (described in the prompt). Your response should be a valid query and
it should be property formatted in Markdown. For example:

**Prompt:** Find all burgers in the `burgers` collection.

```javascript
db.burgers.find({})
```

### Instructions

* Start your `mongo` server
* Connect to the `mongo` shell

### Prompts

**Prompt:** What is the command to start the `mongo` server?

sudo systemctl start mongod    (mongosh) or just nodemon

**Prompt:** What is the command to connect to the `mongo` shell?

mango

**Prompt:** What is the command for listing all `mongo` databases?

show databases

**Prompt:** What command would you use to create a database called `burgers`?

use burgers

**Prompt:** What command would you use to add the collection `burger` to your
`burgers` database?
```javascript
db.burger.insertOne()
```

**Prompt:** What is the command for listing all collections in a database?

show collections

## Inserting

### Prompts

**Prompt:** Insert a single burger into the `burgers` collection with the
following:

* a `patty` property set to `beef`
* a `cheese` property set to `false`
* a `toppings` set to an array with `ketchup`, `onions`, and `pickles` 
```javascript
burgers> db.burger.insertOne({ name: "Cheeseburger", ingredients: ["bun", "beef", "cheese"] })
```

**Prompt:** Insert 10 burgers into the `burgers` collection with the following:

* a `patty` property that is set to one of: `beef`, `turkey`, or `veggie`
* a `cheese` property that is either `true` or `false`
* a `toppings` property that is either one of `ketchup`, `onions`, `pickles`,
  `mustard`, and `mayonnaise
  
  ```javascript
  burgers> db.burgers.insertMany([

   { patty: "beef", cheese: true, toppings: ["ketchup"] },
    { patty: "turkey", cheese: false, toppings: ["onions"] },
   { patty: "veggie", cheese: true, toppings: ["pickles"] },
   { patty: "beef", cheese: false, toppings: ["mustard"] },
   { patty: "turkey", cheese: true, toppings: ["mayonnaise"] },
    { patty: "veggie", cheese: false, toppings: ["ketchup", "onions"] },
    { patty: "beef", cheese: true, toppings: ["pickles", "mustard"] },
    { patty: "turkey", cheese: false, toppings: ["mayonnaise", "ketchup"] },
    { patty: "veggie", cheese: true, toppings: ["onions", "pickles"] },
    { patty: "beef", cheese: false, toppings: ["mustard", "mayonnaise"] }
```

## Reading

The following prompts will have you querying (reading) from your `burger`
collection. If you don't have burgers in your database that match the query
criteria described below, you wont get any results back. So, add one or two that
match that criteria before running the query.

### Prompts

**Prompt:** What query would find all burgers with a `beef` 
patty?
```javascript
db.burgers.find({ patty: "beef" })
```

**Prompt:** What query would find all burgers with cheese on them?
```javascript
db.burgers.find({ cheese: true })
```

**Prompt:** What query would find a burger by it's ObjectId?
```javascript
db.burgers.find({ _id: ObjectId('66a3e0ac06069f861f9f2d67') })
```

**Prompt:** What query would find all burgers with `ketchup` as a topping?
```javascript
db.burgers.find({ toppings: "ketchup" })
```

**Prompt:** What query would find all burgers with either a turkey or veggie
patty?
```javascript
db.burgers.find({ patty: { $in: ["turkey", "veggie"] } })
```

**Prompt:** What query would find all burgers with a beef patty and cheese?
```javascript
db.burgers.find({ patty: "beef", cheese: true })
```

**Prompt:** What query would find all burgers with a beef patty and ketchup as
a topping?
```javascript
db.burgers.find({ patty: "beef", toppings: "ketchup" })
```

**Prompt:** What query would find all burgers with a beef patty and both onions
and pickles as toppings?
```javascript
db.burgers.find({ patty: "beef", toppings: { $all: ["onions", "pickles"] } })
```

**Prompt:** What query would find burgers with either a turkey patty or cheese?
```javascript
db.burgers.find({ $or: [ { patty: "turkey" }, { cheese: true } ] })
```

## Update

### Prompts

**Prompt:** What query would update one burger by it's ObjectId, setting it's
"patty" to "pork"?
```javascript
db.burgers.updateOne( { _id: ObjectId("66a3e0ac06069f861f9f2d67") }, { $set: { patty: "pork" } } )
```

**Prompt:** What query would update all burgers with beef paddies to have
cheese? (i.e. set "cheese" to true)
```javascript
db.burgers.updateMany( { patty: "beef" }, { $set: { cheese: true } } )
```

## Delete

### Prompts

**Prompt:** What query would delete a burger by it's ObjectId?
```javascript
db.burgers.deleteOne({ _id: ObjectId("66a3e0ac06069f861f9f2d67") })
```

**Prompt:** What query would delete all veggie burgers?
```javascript
db.burgers.deleteMany({ patty: "veggie" })
```

**Prompt:** What query would delete all burgers with pickles on them?
```javascript
db.burgers.deleteMany({ toppings: "pickles" })
```
