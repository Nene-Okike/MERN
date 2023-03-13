##  STEP 1 – BACKEND CONFIGURATION

**update ubuntu**
sudo apt update
sudo apt upgrade


**Install nodejs in the server*
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
            node -v
            npm -v
            mkdir Todo
            cd Todo
            npm init
            ls

**Install ExpressJS**

Install express using npm

npm install express

touch index.js
ls

**Install the dotenv module**

npm install dotenv

vim index.js
Copy, paste and save the following codes

const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});

Run node index.js

Output ![]

Open TCP 5000 in the remote server and access express fo=rom the browser with the following command

http://<54.84.181.211>:5000

**Routes**

mkdir routes
cd routes
touch api.js
Copy the below code into the api.js file

const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;


**Models**
npm install mongoose

mkdir models && cd models && touch todo.js
vim todo.js
ls

Copy and save the below code in todo.js file
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;


vin into api.js file in the routes directoty, delete the previous code using 
:%d
and paste and save the below code



const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;


**MongoDB Database**

touch .env
vi .env
paste the code below and save

mongodb+srv://Nelly:<urnwY426C7ypKS5N>@cluster0.kcuhxox.mongodb.net/favourDB?retryWrites=true&w=majority

Run node index.js
This will show that the server is running and connected to te Data base

![]()


Testing Backend Code without Frontend using RESTful API
In this project, we will use Postman to test our API.

 







