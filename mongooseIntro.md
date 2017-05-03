Mongoose
===

Server
---
1) Set up server

2) Install mongoose (terminal)
```
npm install mongoose --save
```

3)Set up Schema
  - node module called a /models/user.js used to define schema (structure of Data)
  - Gives you more structure to data types
  - Seperated from server code 

 user.js
```javascript
  var mongoose = require ('mongoose');
  var Schema = mongoose.Schema;

  var userSchema = new Schema({                 //javascript object
     name: String,                              // field names : Type,
     username: {type: String, unique: true}
     admin: Boolean,
     create_at: Date,
     age: Number
  });
  
 // Tell mongoose to take schema and create a collection
 // Give it a name and the schema just created
 //WARNING: lowercase and plural collection name (1st param)
 var User = mongoose.model('users', userSchema);  
 module.exports = User;
   
```
4) Connect Server to DB
  - mongodb local, default port, name of database creating
  - Default Port: 27017 

server.js
```javascript

  var express = require ('express');
  var mongoose = require ('mongoose');
  var User = require ('./models/user');
  var bodyParser = require('body-parser');
  
  
  var app = express ();
  
  app.use(bodyParser.urlencoded..etc);
  
  mongoose.connect('mongodb://localhost:27017/psiUserDb');
  // psiUserDb is creating the db
  
  app.get('/user', function ( req, res ) {
    
    //calling find method on user schema
    //{} would get all objects - you can add more properties inside to get specific
    
    User.find({}, function(err, userResults) {  
     if(err) {
        console.log(err);
        res.sendStatus(500);
      }else {
        console.log('userResults-->', userResults);
        res.send(userResults);
       }
    })
  });
  
  app.post('/user', function ( req, res ) {
    console.log('in users post', req.body);
    
    var newUser = new User ({
      name: req.body.bob       //name is coming from schema -- bob is coming fom client
      username: req.body.username
     });
    
    //save = insert/create   - takes a callback for once complete
    
    newUser.save( function ( err) {
      if(err) {
        console.log(err);
        res.sendStatus(500);
      }else {
        console.log('new user created');
        res.sendStatus(200);
       }
    })
  })
```






