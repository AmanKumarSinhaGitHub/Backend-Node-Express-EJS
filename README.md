# BackEnd (NodeJs ExpressJs EJS MongoDB)

Steps to setup a backend for any project.

## Express JS Setup

- Use the npm init command to create a package.json file for your application
    ```
    npm init 
    ```

- Now install Express
    ```
    npm install express
    ```


### Hello World Code in ```app.js``` file

- Visit to [npmjs.com](https://www.npmjs.com/package/express) or [expressjs.com](https://expressjs.com/en/starter/hello-world.html) and Copy the boiler plate (hello world) code

    ```js
    const express = require('express')
    const app = express()
    const port = 3000

    app.get('/', (req, res) => {
        res.send('Hello World!')
    })

    app.listen(port, () => {
        console.log(`App listening on port ${port}`)
    })
    ```

## EJS setup

- Install [EJS](https://ejs.co/) 
    ```
    npm install ejs
    ```

- Set view engine
    ```js
    app.set("view engine", "ejs") 
    ```

    Now your code look like this

    ```js
    const express = require('express') 
    const app = express()
    const port = 3000

    app.set("view engine", "ejs")  

    app.get('/', (req, res) => {
        res.send('Hello World!')
    })

    app.listen(port, () => {
        console.log(`App listening on port ${port}`)
    })
    ```
- Create ```views``` Folder
- Create ```ejs``` files inside ```views``` folder
    - Example - ```index.ejs```
    - Inside ```index.ejs```, Paste normal html boilder plate code

        ```html
        <!DOCTYPE html>
        <html lang="en">

        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Index.Js File</title>
        </head>

        <body>
            <h1>Welcome to Index.Js file (Home Route)</h1>
        </body>

        </html>
        ```


### Render ```index.ejs``` file inside route

```js
app.get('/', (req, res) => {
    res.render('index')
})
```

Now your code (```app.js```) look like this.
```js
const express = require('express') 
const app = express()
const port = 3000

app.set("view engine", "ejs") 

app.get('/', (req, res) => {
    res.render('index')
})

app.listen(port, () => {
    console.log(`App listening on port ${port}`)
})
```

### Start the Server
 
Run this command
```
node app.js
```

But, there is a problem in this way. Whenever you made some changes in your file, you have to restart the server again and again to reflect the changes.

So the better approach is to start the server using nodemon

**Install [Nodemon](https://www.npmjs.com/package/nodemon)**

```
npm install nodemon
```

Now to start server, Just type the command given below

```
nodemon app.js
```

### Express static files setup

- Create ```public``` Folder
- Create ```images```, ```stylesheets``` and ```javascripts``` folder inside public folder. 
- You can create files inside these folders. For e.g. ```style.css``` in ```stylesheets``` folder.

Now write this in ```app.js``` file to [serve](https://expressjs.com/en/starter/static-files.html) static files

```js
app.use(express.static('./public'))
```

Now your code (```app.js```) look like this
```js
const express = require('express') 
const app = express()
const port = 3000

app.set("view engine", "ejs") 
app.use(express.static('./public'))

app.get('/', (req, res) => {
    res.render('index')
})

app.listen(port, () => {
    console.log(`App listening on port ${port}`)
})
```
Adding Stylesheet
```html
<link rel="stylesheet" href="/stylesheets/style.css">
```

Now your ```index.ejs``` file looks like

``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Index.Js File</title>

    <!-- Linking stylesheet -->
    <link rel="stylesheet" href="/stylesheets/style.css">
    
</head>

<body>
    <h1>Welcome to Index.Js file (Home Route)</h1>
</body>

</html>
```

And your directory/folder structure looks like this
```
.
├── app.js
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
└── views
    ├── index.ejs

```


<br>

# [EXPRESS GENERATOR](https://expressjs.com/en/starter/generator.html)

You can easily do all the above task by just using express generator and save your time to setting up backend again and again.

#### Install the application generator as a global npm package

```
npm install -g express-generator
```

## Steps to setup

Open cmd/terminal and type the command below to create an app. 
```
express --view=ejs yourAppName
```

Now change directory:
```
cd yourAppName
```


Install dependencies:
```
npm install
```

Now open it on vs code
```
code .
``` 

Your app is created and opened in VS code.

### Run your app by using this command

```
npx nodemon
```


#### Note : directory/folder generated by express generator, structure looks like this 

```
.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug
```

## Some changes that you have to keep in your mind.

1. Previously we write ```app.get```, but now you have to write ```router.get```

2. Previously we start our server using ```npm/npx nodemon yourFileName```, but now we have to write ```npx nodemon``` only.

3. Linking css or other files method remain same.

    ```html
    <link rel="stylesheet" href="/stylesheets/style.css">
    ```
---


# MongoDB

MongoDB is Non-Relational Database.

Here is the table that represent -> If you code then what happen in mongodb


| Code Side  |    | MongoDB Side Action Here |
| -----------|----| ------------------------ |
| DB Setup   | ⟶ | DB Formation             |
| Model      | ⟶ | Collection               |
| Schema     | ⟶ | Documents                |


<br>

### Database Setup == DB Formation
- All the data of an app == Database
- And its setup in code side is called DB Setup and in MongoDb side it is called DB formation.

### Model == Collection
Suppose Amazon have a data base and amazon data base is divided into four parts.

- User DB
- Sales DB
- Admin DB
- Profit DB

These parts are called MODELS in code side and COLLECTION in MongoDB side.

### Schema == Documents
Lets suppose UserDB have users and user must have their name, address and phone no. 

These are called Schema (in code side) and Documents (in mongo db side)

In simple work, how each documents of user look like is called schema


## Lets set up Data Base

Now we are going to setup a database. To do so, we have to follow these steps.

1. Install [MongoDB Community Edition](https://www.mongodb.com/try/download/community) just like any other application

2. Install Mongoose Js

    ```
    npm install mongoose
    ```

3. Require and Setup connection for database

    ```js
    const mongoose = require("mongoose")

    // Connect to local host mongodb server 
    mongoose.connect("mongodb://127.0.0.1:27017/amazonDB")
    // The above line create a database in mongodb named "amazonDB"
    ```

4. Make Schema (Document)

    ```js
    const userSchema = mongoose.Schema({
        username: String,
        name: String,
        age: Number
    })
    ```

5. Create Model (collection) and Export

    ```js
    module.exports = mongoose.model("userDB", userSchema)
    ```

So what we did? 
- We created a Database names ```amazonDB```, means Data Setup in code side and DB formation in MongoDB side.
- We created a model (in code side) or collection (in mongodb side) named ```userDB```. 
- We created a document that contains data format about user, means Schema created in code side named ```userSchema``` and document created in mongodb side.


### DATABASE Structure

```
── amazonDB
        └── userDB
                └── userSchema
```

### Now lets do operations in db

write this code in user.js file

```js
const mongoose = require("mongoose")

// Connect to local host mongodb server 
mongoose.connect("mongodb://127.0.0.1:27017/amazonDB")
// The above line create a database in mongodb named "amazonDB"

const userSchema = mongoose.Schema({
  username: String,
  name: String,
  age: Number
})

module.exports = mongoose.model("userDB", userSchema)
```


And in index.js to create db
```js
var express = require('express');
var router = express.Router();

// Importing mongodb setup code that is written in user.js
const userModel = require("./users")

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index');
});

// Creating model. 
router.get("/create", async function (req, res){
  const createdUser = await userModel.create({
    // these are schema details
    username: "aman",
    name: "aman kumar sinha",
    age: 20
  });
  res.send(createdUser);
})
// Note: all the things related to userModel is asynchronous nodejs function. So always write async and await

module.exports = router;
``` 

When you visit ```http://localhost:3000/create``` your data base will be created.

To see the database is created or not. Open terminal. Type command 
```
mongod
```
This will open your mongodb server.
Then open a one more tab or a new terminal and type command.
```
mongosh
```
And after that in same terminal type these commands one by one
```js
// This command show all the db in your computer
show dbs

// Now go to the db that you have created. In our case, its amazonDB
use amazonDB

// Now write this command to see all the collection inside amazon db
show collections

// Now type this to see what is in userdb collection
db.userdbs.find()

// Your userdb's user data look like this
[
  {
    _id: ObjectId("65411c6ea1039336d4d364cc"),
    username: 'aman',
    name: 'aman kumar sinha',
    age: 20,
    __v: 0
  }
]
```

To read data using nodejs code (add this line in index.js)

```js
// See data (READ data)
router.get("/allUser", async function(req, res){
  let users = await userModel.find()
  res.send(users)
})

```
Go to ```localhost:3000/allUser``` to read data

Note: ```.find()``` return you all the use. ```.findOne()``` return you one user.

```js
router.get("/allUser", async function(req, res){
  let users = await userModel.findOne({username:"aman"})
  res.send(users)
})
```

Delete Data code
```js
// DELETE Data
router.get("/delete", async function(req, res){
  let deletedUser = await userModel.findOneAndDelete({
    username:"aman"
  })
  res.send(deletedUser)
})
// the above code will find user that username is aman and delete it and return its data to deletedUser variable
```

### [Session](https://www.npmjs.com/package/express-session) and [cookies](https://www.npmjs.com/package/cookie-parser):
Data that saved on client side is called cookies and the data that saved on server is called session.

To use session, you need to install a package form npm
```
npm install express-session
```

In app.js write some lines to use express-session

```js
const session = require('express-session');

app.use(session({
  secret: 'your-secret-key-here', // A secret key to sign the session ID cookie
  resave: false, // means if data is not modified, don't resave.
  saveUninitialized: false // means don't save uninitailized data
}));
```

now you can make/create session (open index.js file)

```js
// In any route you can set session.
// in our session session is set in home route and if someone visit our home route, session will create and if you open checkSession route, you can see session.

router.get('/', function(req, res, next) {

    // Session code here
    req.session.anyExampleNameHere = 'exampleUserData'; // Storing user data in the session

    res.render('index');
});

// READ Session
router.get('/checkSession', function(req, res){

    if(req.session.anyExampleNameHere == "exampleUserData"){
        console.log(req.session)
        res.send("Session saved. see on your console/terminal")
    }
    else{
        res.send("Session data is not available or deleted")
    }
    
})
```

To delete session, code is here
```js
// Deleting/Destroy session
router.get("/removeSession", function(req, res){
  req.session.destroy(function(err){
    if(err) throw err;
    res.send("session deleted")
  })
})
```

### Cookies-Parser

Cookies are already setup in your code by exress generetor, still I am proving the code

```js
var cookieParser = require('cookie-parser');

app.use(cookieParser());
```

Create and read cookie code (index.js)

```js
router.get('/', function(req, res, next) {

  // Cookies code here
  res.cookie("nameHere", "valueHere")

  res.render('index');
});

// Read cookie

router.get('/checkCookie', function(req, res){
  console.log(req.cookies)
  res.send("check console/terminal for cookie")
})

// Delete cookie

router.get('/deleteCookie', function(req, res){
  res.clearCookie("nameHere")
  res.send("cleared cookie")
})

```

### This is all about backend. Thank You...