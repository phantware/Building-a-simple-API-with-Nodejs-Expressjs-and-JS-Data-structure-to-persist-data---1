# This tutorial is for building simple API with Nodejs using ES6.

## I created this as a guide for myself

## 
What we will build?
You'll learn how to build a reflection API - A reflection app gives users the ability to reflect and document daily 
successes, failures and a plan on what to do better the next day.

the Technology we are going to use is
a) Node.js
b) Express js

1. I first create a folder called node_express_tutorial
2. I then do npm init to initialize package.json and I fill in the necessary details accordingly
3. Next, I then install all the package dependencies that we'll need to build the project which are:

expressjs - Expressjs is a nodejs web application framework that gives us the ability to create quick and easy APIs.
momentjs - This gives us the ability to validates and manipulates dates.
uuid npm package
babeljs - Since we'll be writing all our JavaScript code using ES6, babeljs will help in converting our ES6 codes to ES5.
babel watch - This is needed for development. One thing that babel watch package does is to compile our code and reload the server each time we make changes to our code.

4. We then run the following code
 npm install --save express moment uuid (Search for the latest version)
 npm install --save-dev babel-cli babel-preset-env babel-watch (Search for the latest version)

You'll notice that express and moment is under dependencies, that is because those are needed by the time we deploy our code to production. babel-cli, babel-preset-env and babel-watch are only needed during development.

5. Then I set my project module to look like the following format
-node_express_tutorial
  |-package.json
  |-.babelrc
  |-server.js
  |-src
    |-controllers
      |-Reflection.js
    |-models
      |-Reflection.js

6. I then set up the server
      Explanation on what I set up on the server
a. I imported express and set up a new express instance const app = express(). 
b. I set up a new express.json() middleware - this is needed to get access to request body. 
c. Lastly, we set up a sample endpoint to test if the server is working.
Note: express.json() is only available in express version 4.16.0 and above

If you run the server using node server.js command, you'll get an error


7. I then setup babel to conver ES6 to ES5. In the project root directory, I then create a file and name it .babelrc
8. Next, open package.json and add "build": "babel server.js --out-dir build" under script property.
9. I then run the code npm run build
10. If the above command was successful you will notice that a new build folder has been created in the project directory.
 Open it and click on server.js - notice the original code has been compiled down to es5. So, running the server.js 
 inside build folder should successfully run your server without error.

 11. Run the below code
  node build/server.js

  12. I then add the below code to my package.json under the script to automatically reload my server 
  "dev-start": "babel-watch server.js"
  13. I then ran npm run dev-start but yarn run dev-start is it equivalent
  14. when I got message that @babel/core is not installed, I did yarn add @babel/core --dev` to install it
15. I faced so many errors running my server after all the settings has been done.
    so I install all the followings in my Devdependencies
    
    yarn add @babel/cli --dev
    yarn add @babel/preset-env --dev
    yarn add @babel/node --dev
    yarn add --dev babel-watch
    yarn add @babel/core --dev

  16. I also replace the .babelrc code with the following
      {
    "presets": [ "@babel/preset-env"]
}

// after all the errors has been fixed, I now continue below
16.a. Next, open package.json and add "build": "babel server.js --out-dir build" under script property.
16.b. Now, run the following command

$ yarn run build
Note: If this code ran succeffuly, you will notice that a new build folder has been created in the project directory.
Open it and click on server.js - notice the original code has been compiled down to es5. So, running the server.js inside build folder should successfully run your server without error.

16.c. We then run node buil/server.js
16.d. I then set up babel watch to watch over any changes we made in our code and automatically compile and restart our server.
   Add "dev-start": "babel-watch server.js" to your package.json under script.
   Running npm run dev-start should start your server

  17. I then Set up Reflection Model
          To make things simple, we'll not make use of database for our project. 
          Instead we'll use JavaScript Objects to persist user's data.
          Open src/models/Reflection.js and add the following code, the code can be found in Reflection.js
18. Meaning of all the parameters in the code
        We created Reflection class with five methods 
        a) create() - to create a new reflection, 
        b) findOne() - find one reflection, 
        c) findAll() - find all reflections, 
        d) update() - update a reflection and 
        e) delete() - delete a reflection. 
        Each reflection object will contains six propeties id, success, lowPoint, takeAway, createdDate and modifiedDate.
        We use uuid.v4() to set the default reflection id, moment to set default values for createdDate and modifiedDate.
19.  We now Set up Controller and Endpoints
     The following endpoints will be defined
    Create a Reflection - POST /api/v1/reflections
    Get All Reflections - GET /api/v1/reflections
    Get A Reflection - GET /api/v1/reflections/:id
    Update A Reflection - PUT /api/v1/reflections/:id
    Delete A Reflection - DELETE /api/v1/reflections/:id
    But first, let's set up our reflection controller, to do that add the following code to src/controllers/Reflection

20. We setup our reflect controller to and we write code inside
  We created Reflection object that contains create - to create a new reflection, 
  getAll - get all reflections, 
  getOne - get one reflection, 
  update - update a reflection and 
  delete - delete a reflection properties.
21. Finally, let's defined our endpoints, open server.js and add the following code


Finally, let's defined our endpoints, open server.js and add the following code
