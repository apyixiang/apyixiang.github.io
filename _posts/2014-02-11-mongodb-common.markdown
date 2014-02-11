---
layout: post
title: "mongodb常用操作"
date: 2014-02-11 14:06
comments: true
categories: dev
tags: [mongodb]
---

db.collection.update({}, {$rename: {'field1': 'field2'}}, false, true);
db.collection.renameCollection('new_collection')
db.collection.distinct('filed')

db.createCollection("noautoid", { autoIndexId: false })


http://stackoverflow.com/questions/12378320/mongodb-inserting-doc-without-id-field

By default, all regular collections automatically insert an _id field if it is absent.

However, this behavior can be changed when you create the collection, by setting explicitely the autoIndexId parameter to false.

```
> db.createCollection("noautoid", { autoIndexId: false })
{ "ok" : 1 }
Then you can insert documents without _id field. But some drivers, like the javascript one (and so the mongo console), add the _id field by themselves. In the mongo console, you can do this:

> db.noautoid._mongo.insert(db.noautoid._fullName, {name: "Jack"})
> db.noautoid.find()
{ "name" : "Jack" }
More information about the autoIndexId field can be found in the MongoDB documentation. This page is about Capped Collections but the autoIndexId field is common to both regular and capped collections.
```