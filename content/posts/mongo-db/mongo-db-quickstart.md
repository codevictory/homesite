---
title: 'Mongo Db Quickstart'
date: 2020-07-07T22:27:27+03:00
author: 'codevicory'
description: 'Absolute minimal quickstart for using MongoDB.'
draft: false
---

Document orientated database with JSON-like syntax.

## Document datastructure

![Relational datastructure vs. document datastructure](/images/relational-vs-document.png)
source: http://prabathsl.blogspot.com/2013/02/document-oriented-database_14.html

### Basic structure

```json
{
  "name": "Markus",
  "age": 27,
  "place": "Merimasku",
  "status": "On holiday",
  "computer": {
    "os": "MacOS",
    "year": 2018
  }
}
```

## Development Tools

- [Compass](https://www.mongodb.com/products/compass) (GUI)
- [MongoDb Shell](https://www.mongodb.com/products/shell) (command line tool)

## Commands

Basic CRUD capablities.

### Query data

Return all documents which "title" key's value is "Post One".
`[database name].[collection name].find({ "title": "Post One" })`

### Insert data

Add one:

```json
db.posts.insert({
  "title": "Post One",
  "body": "Body of post one",
  "category": "News",
  "tags": ["news", "events"],
  "user": {
    "name": "John Doe",
    "status": "author"
  },
  "date": Date()
})
```

Add many:

```json
db.posts.insertMany([
  {
    "title": "Post Two",
    "body": "Body of post two",
    "category": "Technology",
    "date": Date()
  },
  {
    "title": "Post Three",
    "body": "Body of post three",
    "category": "News",
    "date": Date()
  },
  {
    "title": "Post Four",
    "body": "Body of post three",
    "category": "Entertainment",
    "date": Date()
  }
])
```

### Update document

```json
db.posts.update(
  { "title": "Post Two" },
  {
    "$set": {
      "title": "Post Two",
      "body": "New body for post 2",
      "date": Date()
    }
  },
  {
    "upsert": true
  }
)
```

### Remove document

Remove all which have status of "A".

```
db.inventory.deleteMany({ status : "A" })
```

Remove first which have status of "A".

```
db.inventory.deleteOne({ status : "A" })
```

### Operators

MongoDB offers various operators and functions out-of-the-box. Operators are being stated with \$-symbol and functions like `Date()`.

Example: Return all the documents which contain word "cat".

```
db.posts.find({
  $text: {
    $search: "\"cat\""
    }
})
```

## Tutorial & further reading

YouTube Crash Course:  
https://www.youtube.com/watch?v=-56x56UppqQ

MongoDB Cheat Sheet:  
https://gist.github.com/bradtraversy/f407d642bdc3b31681bc7e56d95485b6
