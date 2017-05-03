Mongoose
===

Server
---
1) Set up server

2) Install mongoose (terminal)
```
npm start mongoose --save
```

3) Set up Schema
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
