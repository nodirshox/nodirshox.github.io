---
layout: post
title: "How to create nested MongoDB models via Mongoose package"
categories: ["tutorial", "programming", "nodejs"]
permalink: /how-to-create-nested-mongodb-models
---

![Screenshot](/assets/2021-03-06-mongodb-model/nested.jpg)

Mongo DB database is very flexible with different data types, such as nested objects and arrays. We have an awesome tool for designing schema in Node JS. It is called Mongoose. In this post, we will discover the features of Mongoose.

My first to do is create schema for models when I started a new project. One of the preferred path of the project, it is saving all schemas in "models" folder. Let me give sample schema for this tutorial.


# Post Model

```
title - String
author - String
body - String
status - Enumerator ("PENDING", "PUBLISHED")
view_count - Number
created_at - Date
```

Before writing Mongoose schema, make sure you have installed package by:

```
npm install mongoose --save
```

Let's go straightforward and write our schema.

/models/Post.js

```
const mongoose = require('mongoose');

var PostSchema = new mongoose.Schema({
    title: {
        type: String,
        required: true
    },
    author: {
	type: String,
	required: true
    },
    body: {
        type: String,
        default: ''
    },
    status: {
	type: String,
	enum: ["pending", "published"]
	default: "pending"
    },
    view_count: {
	type: Number,
	default: 0
    },
    created_at: {
        type: Date,
	default: Date.now
    }
});

module.exports = mongoose.model('Post', PostSchema);
```

It is a very simple schema for now. But we can add complex nested schemas, pre-save method, build-in validations, and so on.

Let add a category of the blog in schema. But we will add category schema as parent and blogs will be children of category.

```
const mongoose = require('mongoose');

var PostSchema = new mongoose.Schema({
    ...
});

var CategorySchema = new mongoose.Schema({
    title: {
	type: String,
	required: true
    },
    posts: [ PostSchema ],
    created_at: {
        type: Date,
	default: Date.now
    }
});


module.exports = mongoose.model('Category', CategorySchema);
```

As you can see, now we have one document of category, and posts will be placed as an array of objects of a category. You can up to 100 nested levels which limited by MongoDB.

Mongoose also provides other facilities, such as querying, populating data, validation. For more info visit Mongoose [documentation](https://mongoosejs.com/){:target="_blank"}.

If you interested in CRUD operation using Mongoose and Node JS, please visit [this post](https://ergashevn.blogspot.com/2020/09/node-js-express-mongodb-crud.html){:target="_blank"}.

If you have any question regarding Mongoose, you can reach via mr.nodirbek77@gmail.com.

[Link](https://ergashevn.blogspot.com/2021/03/how-to-create-nested-mongodb-models-via.html){:target="_blank"}
