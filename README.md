# setup
# UNIT 2

## Steps to create node App
- Open a new terminal
- Create a new folder and cd into that folder
- 'npm init' is to create package.json/keep pressing enter
- 'npm init -y' is to create package.json/skips all the steps
- create a index.js file in the terminal('touch index.js)
- Open folder in vs-code
- Create a myModule.js file
    module.exports is an object that will hold the code to be exported. We can use dot-notation to add the code we want to export to this object.
- Inside the myModule.js file add
    the code module.exports.beBasic = () => "That's so fetch!"
    Import the code from myModule that is beimg exported
-const myModule = require('./myModule.js');
-console.log(myModule.beBasic());
- 'node index.js' is use to run the file
##### fs(file system) to read a text file
    const fs = require('fs')
    Can be written as
    fs.readFile('story.text', 'utf8', (err, data) =>{
        if(err) {
            console.log("There was a problem reading the file")
        } else {
            console.log(data)
        }
    })
    Run index.js to read your story in the terminal!

## Installing NODEMON
- Open a new terminal
- npm i -g nodemon

## Installing MOMENT
- Open a new terminal
- npm i moment

## Steps to create Express App
- Open a new terminal    
- Create a new folder and cd into that folder
- 'npm init' is to create package.json/keep pressing enter
- 'npm init -y' is to create package.json/skips all the steps
- create a index.js file in the terminal('touch index.js)
- Install express('npm i express')
- echo "node_modules" >> .gitignore
- Open folder in vs-code
Import the Express module in index.js file(or the main .js file)
- const express = require('express');
##### Create an instance of an express app
- const app = express();
#####    create a Home Route
- app.get('/', (req, res) => {
res.send('Hello, World!');
});
##### Add a port 
- app.listen(8000);
     Run nodemon in the Terminal to checking if its listening
- nodemon
### Routes
    Parameters
    By putting a colon before a string in our route, we can create routes with different variables, or parameters
    - app.get('/', (req, res) => {
    res.send("You've reached the home route!");
    });

- app.get('/about', (req, res) => {
  res.send('This is a practice app to learn about express routes.');
    });

- app.get('/:input', (req, res) => {
  console.log("req.params: ", req.params)
  res.send("Our parameter is " + req.params.input + ".");
    });
- app.get("/greet/:name/:lastname", (req, res) => {
  res.send("Hello " + req.params.name + " " + req.params.lastname);
});

#### Views Folder
- Create a views folder
- Add the ejs files to the folder
- In the route, connect it tothe ejs files
- app.get('/', (req, res) {
  res.sendFile('index.ejs');
});

## Steps to create a Template
- First create an express app
- Install EJS 'npm i ejs'
- Set the view engine to EJS
app.set('view engine', 'ejs');
- Create an object with at least one key-value pair and pass that object in as the second argument to the render function in one of your routes:
app.get('/', (req, res) => {
    res.render('index.ejs', {name: 'Sterling Archer', age: 35})
})
- We can access this variable by embedding it into the html using this notation: <%= embedded js goes here %>
The addition of the = sign on the opening tag means that a value will be printed to the screen.


## Layouts & Controllers
### Layouts
- Set Up a Express App
- Initialize Node
- Install Dependencies(express and ejs)
- Set up EJS
- Install EJS layouts('npm i express-ejs-layouts')
- Require the module and add it to the app.
'const ejsLayouts = require('express-ejs-layouts');'
app.use(ejsLayouts);
- Create a layout.ejs file in the view folder
- Create a HTML Template in the layout file. Insert the code '<%- body %>' in the body tag
### Controllers
- Change routes to have the following url patterns: /name of js file in controller/food

- Create a controller folder inside the root directory
- Inside the controller folder. Create a js file(eg.loveit.js)
- In the js file enter const express = require('express');
- In the js file enter const router = express.Router();
- copy the routes into this file.
change app to router
router.get('/lovit/foods', (req, res) => {
  res.render('foods', {foods: ['coconut', 'avocado']});
});
- At the end of the page enter
module.exports = router;

### CRUD METHODS
#### GET
- GET is a read only method
##### New Route
- Write a GET route in the index.js or controller folder(if there is one).
Reads and list all the value.
 router.get('/new', (req, res)=>{
    res.render('dinosaurs/new')
})
- Create a new.ejs file in the views folder
- In the index.ejs create a form with the GET Method
'form method='GET' action=' '>'

#### Post
- Create method
##### Create Route
- Write a POST route in the index.js or controller folder(if there is one).
- Redirects to the GET ejs

#### PUT
- Update Method
##### PUT route
- Write a PUT route in the index.js or controller folder(if there is one).
- router.get('/edit/:idx', (req, res) => {
    res.render(''/edit', data
})
- Create a edit.ejs file in the views folder
- In the edit.ejs create a form with the PUT Method
'form method='PUT' action=' '>'

#### Delete
- Delete Method
##### Delete route
- Write a DELETE route in the index.js or controller folder(if there is one).
- router.delete('/:idx', (req, res) => {
    res.redirect('/ejs folder')
})

### SET UP SEQUELIZE

Setup part 1 - getting the sequelize-cli tool (you only have to do this once)

We need install a generator so we can use sequelize. Much like our other terminal apps, we will only install this once. npm install -g sequelize-cli

Setup part 2 - starting a new node project

Let's build our first app using Sequelize! First we need to create a node app and include our dependencies. All in terminal: Create a new folder and add an index.js and .gitignore and initialize the repository

mkdir userapp

cd userapp

npm init -y

touch index.js

echo "node_modules" >> .gitignore
Add/save dependencies (sequelize needs pg for Postgres)

npm install pg sequelize
Initialize a sequelize project

sequelize init
For your historical reference...

WARNING (2017) Edited (2018): At one point, sequelize-cli, sequelize, and pg modules were not playing nicely with each other. Luckily, this issue (for version Sequelize 4) has been resolved and we can resume using the current versions of both. In the future, be mindful that many modules you use are maintained by individual third parties and issues like this may come up!

If you used to use Sequelize 3, keep in mind that Sequelize 4 has breaking changes! If you need to upgrade your app, refer to these docs, which guide you in the update process.

Setup part 3 - config.json, models and migrations:

In the text editor we should now see a bunch of new folders. We now have config, migrations and models. This was created for us when we ran sequelize init. Let's start in the config folder and open up the config.json file. This file contains information about the database we are using as well as how to connect. We have three settings, one for development (what we will use now), test (for testing our code), and production (when we deploy our app on AWS/Heroku). Let's change the config.json so it looks like this.

config/config.json
{
  "development": {
    "database": "userapp_development",
    "host": "127.0.0.1",
    "dialect": "postgres"
  },
  "test": {
    "database": "userapp_test",
    "host": "127.0.0.1",
    "dialect": "postgres"
  },
  "production": {
    "database": "userapp_production",
    "host": "127.0.0.1",
    "dialect": "postgres"
  }
}
If the dialects defaults to mySql, change them to postgres change the database names

If you have a username and password for your Postgres server, you must include those as well

When we deploy to Heroku, they will provide us a long url that contains password and login that will be secure when deployed. More on this later. Once this is complete, let's move to the models folder.

Create a database inside of Postgres

The sequelize CLI has an equivalent command to createdb. You can use either, they do the same thing!

sequelize db:create userapp_development

Create a model and a matching migration

In order to create a model, we start with sequelize model:create and then specify the name of the model using the --name flag. Make sure your models are always singular (table name in plural, model name in singular). See the Table Name Inference section of [these docs](https://sequelize.org/master/manual/model-basics.html#:~:text=Models are the essence of,(and their data types)for more. After passing in the --name flag followed by the name of your model, you can then add an --attributes flag and pass in data about your model. Generating the model also generates a corresponding migration. You only need to do this once for your model.

sequelize model:create --name user --attributes firstName:string,lastName:string,age:integer,email:string
Make sure you do not have any spaces between each of the attributes and their data types. Convention matters! This will generate the following model:

models/user.js
'use strict';
const {
  Model
} = require('sequelize');
module.exports = (sequelize, DataTypes) => {
  class user extends Model {
    /**
     * Helper method for defining associations.
     * This method is not a part of Sequelize lifecycle.
     * The `models/index` file will call this method automatically.
     */
    static associate(models) {
      // define association here
    }
  };
  user.init({
    firstName: DataTypes.STRING,
    lastName: DataTypes.STRING,
    age: DataTypes.INTEGER,
    email: DataTypes.STRING
  }, {
    sequelize,
    modelName: 'user',
  });
  return user;
};
If you want to make changes to your model after generating it - all you have to do is make a change in this file and save it before running the migrate command. And a corresponding migration:

migrations/*-create-user.js
'use strict';
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('users', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      firstName: {
        type: Sequelize.STRING
      },
      lastName: {
        type: Sequelize.STRING
      },
      age: {
        type: Sequelize.INTEGER
      },
      email: {
        type: Sequelize.STRING
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },
  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('users');
  }
};
What is this "associate" thing in my model?

In this function, we specify any relations/associations (one to one, one to many or many to many) between our models (hasMany or belongsTo). We'll discuss this more, but always remember, the association goes in the model and the foreign keys go in the migration.

Running the migration

To run the migration, use the following command in your VSCODE terminal:

sequelize db:migrate
If you need to undo the last migration, this command will undo the last migration that was applied to the database.

sequelize db:migrate:undo
Use the psql shell to verify that your database and table was created:

psql
\l
\c userapp_development
\dt
