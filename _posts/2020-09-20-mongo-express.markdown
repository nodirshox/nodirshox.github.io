---
layout: post
title: "Node JS Express MongoDB CRUD"
categories: ["tutorial", "nodejs"]
permalink: /node-js-express-mongodb-crud
---

![Poster](/assets/2020-09-20-mongo-express/poster.jpg)

If you just starting just simple web application using Node.js and you don't know what to do, you are lucky, let's go.

Let's discuss stack which are we are going to use in the article.

[Node.js](https://nodejs.org/en/){:target="_blank"} - Backend

[MongoDB](https://www.mongodb.com/){:target="_blank"} - NoSQL database

[Mongoose](https://mongoosejs.com/){:target="_blank"} - npm package for building models

[Express](https://expressjs.com/){:target="_blank"} - a minimal web framework

# Requirements

The most essential soft, we are going to use is Node.js. If don't have a Node in your machine, please take the time and install it. We can verify it by typing command in your terminal(in Windows Command Prompt).

```
node -v
```

If terminal shows, some number, you are good to go. Currently, I have v8.10.0.

# Hello World

Firstly, create a folder and open it in your favorite text editor. In my case, [VS Code](https://code.visualstudio.com/){:target="_blank"}.

Type below in terminal, this helps to us create simple package.json file. It stores essential information for our project.

```
npm init --y
```

Our task is to create a very basic web page which says 'Hello World!'. That's why we need to create a server file. As mention above, we are going to use Express framework for building web pages.

[Express](https://expressjs.com/){:target="_blank"} is one of famous minimal web framework for Node.js. We can install Express package by typing this:

```
npm install --save express
```

If you noticed that, it created a folder called 'node_modules'. This folder stores all package files.

Create a file called server.js in your main directory. Let's code it with simple server.

```
const express = require('express')
const app = express()

app.get('/', function(req, res) {
    res.send('Hello World!')
})

const port = 3000
app.listen(port, () => {
    console.log('Server started on port', port)
})
```

First two lines code is used for calling express package create variable called 'app'.

Next part of code, we asked for response in main url which is '/' and waited for GET response. Then we send simple text to the browser.

Last part, we launched our our server by listening port 3000.

Save this file and launch our server by:

```
node server.js
```

Let's try out in browser and visit:

```
http://localhost:3000
```

Yauhhh. We created first amazing website.

(you can stop server by pressing CTRL + C)

# Connecting database

Let's install 2 packages before connecting database.

```
npm install --save mongodb mongoose
```

There 2 options for database set up

1. Connect free MongoDB database (free limit ~500 MB)
2. Install local MongoDB app, use it for locally


Both of them good, I 1-option when we are going do deploy app. 2-option for development stage. I used 2-option in the lesson.

Let's add those code in our server.js file after 3rd line of code:

```
// Connecting database
DB_URL = 'mongodb://localhost:27017/todo'
mongoose.connect(DB_URL, { useNewUrlParser: true, useUnifiedTopology: true, useFindAndModify: false, useCreateIndex: true })
mongoose.connection.once('open', () => {
    console.log('Connected to database');
}).on('error', (error) => {
    console.log(`There is an error in connecting database: ${error}`);
});
```

You can change database link if you are connecting to online MongoDB database.

Start your server by typing 'node server', if it says **'Connected to database'**, we can move forward.

# To Do App

Move on more complex app, we will enter some data to our application and save it for our database. Then we can do CRUD operation which stands for:

C - create

R - read

U - update

D - delete

We have an awesome package called [Mongoose](https://mongoosejs.com/){:target="_blank"}. We can implement complex models with less coding.

Let's create folder called 'models' and file 'Task.js' in on it.

After that, our directory looks like:

![VS Code](/assets/2020-09-20-mongo-express/vscode.jpg)

Let's discuss our model we are going to implement it. We will have 3 fields for our model:
title - String
body - String

is_active - Boolean

Let's implement our Task model, open models/Task.js write this down:

```
const mongoose = require('mongoose')

var TaskSchema = new mongoose.Schema({
    title: {
        type: String,
        required: true
    },
    body: {
        type: String,
        default: ''
    },
    is_active: {
        type: Boolean,
        default: true
    }
});

module.exports = mongoose.model('Task', TaskSchema);
```

You can learn how to implementing model schema by those code.

Types of data: String, Boolean, Number, Date, ...

If we add 'required: true' in our field, by definition it asks for data is required.

If you needs to add default value for your model, you can do it by adding default section.

And do not forget export your model in the end of file.

You can also add nested schema and arrays using Mongoose, but for now, let's keep it simple.

Add Router
Now are adding more routes, it good style separate route codes from server file. Let's delete 'app.get' function and add this below. You can get full code from [repository](https://github.com/nodirshox/nodejs-mongodb-crud){:target="_blank"}.

```
// Route
const router = require('./router.js')
app.use('/', router)
```

Let's create router.js file in main folder and add this:

```
const express = require("express")
const router = express.Router()

router.use('/', function(req, res) {
    res.send('Hello World!')
});

module.exports = router
```

Let's launch our server to check whether it works or not.

We have simple routes for To Do App

/ - list of tasks

/create - create

/123 - single task by id

/update/123 - update task by id

/delete/123 - delete task by id

Now, we are ready to go implement routes in router.js file:

```
const express = require("express")
const router = express.Router()
const Task = require('./models/Task')

// List of tasks
router.get('/', (req, res) => {
    Task.find({}).exec((err, tasks) => {
        res.send(tasks)
    })
});

// Create
router.get('/create', (req, res) => {
    res.render('create')
})

router.post('/create', (req, res) => {
    var task = new Task(req.body);
    task.save().then(item => {
    	res.send(item)
    })
})

module.exports = router
```

It is almost ready to use, but we need set up before testing it.

Install 'ejs' package for using template engine

```
npm install ejs --save
```

And this code in server.js before adding router

```
// Template engine
app.set('views', 'views');
app.set('view engine', 'ejs');
var bodyParser = require('body-parser');
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
```

And create folder 'views' and file 'create.ejs' inside. Add this simple form:

```
<form action="/create" method="POST">
    <label>Title</label>
    <input type="text" name="title">
    <br>
    <label>Description</label>
    <input type="text" name="body">
    <br>
    <input type="submit" value="SAVE">
</form>
```

And now we can go to

```
http://localhost:3000/create
```

![Form](/assets/2020-09-20-mongo-express/example.jpg)

It will return raw formatted data. But, we create a beautiful HTML & CSS page and put this data on-page. I implemented rest operation (get task, update, delete) in router file. You can use the [repository](https://github.com/nodirshox/nodejs-mongodb-crud){:target="_blank"}.

I hope you got the basic idea of creating Node.js app. If you have any questions/improvements, feel free to contact me by email (mr.nodirbek77@gmail.com).

**Rock on!**

[Link](https://ergashevn.blogspot.com/2020/09/node-js-express-mongodb-crud.html){:target="_blank"}