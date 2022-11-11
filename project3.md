## Documentation for Project 3: MERN STACK IMPLEMENTATION

**Preparing prerequisites**

- Create a new EC2 Instance of t2.nano family with Ubuntu Server 20.04 LTS (HVM) image.

1. **Backend Configuration**

- Update ubuntu

`sudo apt update`

![Ubuntu Update](./image/ubuntu-update-output.PNG)

- Upgrade ubuntu

`sudo apt upgrade`

![Ubuntu Upgrade](./image/ubuntu-upgrade-output.PNG)

Lets get the location of Node.js software from Ubuntu repositories.

`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

![Nodejs Ubuntu Repo](./image/nodejs-ubuntu-repo-output.PNG)

- Install Node.js on the server
Install Node.js with the command below:

`sudo apt-get install -y nodejs`

![Nodejs Installation](./image/install-nodejs-output.PNG)

- Note: The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

- Verify the node installation with the command below:

`node -v `

![Node Version Info](./image/node-version.PNG)

- Verify the node installation with the command below:

`npm -v `

![Npm Version Info](./image/npm-version.PNG)

- Application Code Setup
Create a new directory for your To-Do project:

`mkdir Todo`

![Create Todo Directory](./image/todo-directory.PNG)

- Run the command below to verify that the Todo directory is created with ls command:

`ls`

![ls Output](./image/ls-output.PNG)

Now change your current directory to the newly created one:

`cd Todo`

![Directory Change to Todo](./image/change-directory-todo.PNG)

- Next, you will use the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

`npm init`

![Npm Init Output](./image/npminit-output.PNG)

![Npm Init Output](./image/npminit-output2.PNG)

- Run the command ls to confirm that you have package.json file created:

`ls`

![Package Json Output](./image/package-json-status.PNG)



2. **Install ExpressJS**

- Remember that Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.

- To use express, install it using npm:

`npm install express`

![Npm Install Express](./image/npm-install-express.PNG)

- Now create a file index.js with the command below:

`touch index.js`

![Create Index.js](./image/touch-index-output.PNG)

- Run ls to confirm that your index.js file is successfully created

`ls`

![Index.js Success Confirmation](./image/indexjs-success-output.PNG)

- Install the dotenv module:

`npm install dotenv`

![Npm Dotenv Install](./image/npm-dotenv-install.PNG)

- Open the index.js file with the command below:

`vim index.js`

- Type the code below into it and save. Do not get overwhelmed by the code you see. For now, simply paste the code into the file.

![Vim Code Input](./image/vim-command.PNG)

- Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:

`node index.js`

![Node Server Output](./image/node-server-success.PNG)

- Now we need to open this port in EC2 Security Groups. Refer to Project 1 Step 1 – Installing the Nginx Web Server. There we created an inbound rule to open TCP port 80, you need to do the same for port 5000, like this:

![Inbound Rule Output](./image/inbound-rule-output.PNG)

- Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:

[5000 Browser Success](http://3.141.168.107:5000/)

![Express Confirmation](./image/express-confirm-output.PNG)

- Routes
There are three actions that our To-Do application needs to be able to do:

Create a new task
Display list of all tasks
Delete a completed task
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

- For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes:

`mkdir routes`

![Routes Create Directory](./image/routes-directory-output.PNG)

- Change directory to routes folder:

`cd routes`

![Routes Create Directory](./image/change-to-routes-directory.PNG)

Now, create a file api.js with the command below:

`touch api.js`

![Apijs Output](./image/apijs-output.PNG)

Open the file with the command below:

`vim api.js`

![Vim Code Copy](./image/vim-code-copy.PNG)


3. **Models**

- Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document. (Seems like a lot of information, but not to worry, everything will become clear to you over time. I promise!!!)

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

- Change directory back Todo folder with cd .. and install Mongoose:

`cd ..`

![Change back to Todo Directory](./image/change-back-todo.PNG)

`npm install mongoose`

![Install Mongoose Success Output](./image/mongoose-install-output.PNG)

- Create a new folder models :

`mkdir models`

![Create Models Directory Output](./image/models-output.PNG)

- Change directory into the newly created ‘models’ folder with:

`cd models`

![Change to Models Directory](./image/change-to-models-directory.PNG)

- Inside the models folder, create a file and name it todo.js:

`touch todo.js`

![Todojs file create](./image/todojs-create-output.PNG)

- Tip: All three commands above can be defined in one line to be executed consequently with help of && operator, like this:

`mkdir models && cd models && touch todo.js`

![Models Todojs Output](./image/models-todojs-output.PNG)

- Open the file created with vim todo.js then paste the code below in the file:

`vim todo.js`

![Todo Schema Model Create](./image/todo-schema-model-create-output.PNG)

- Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit:

In the index.js file, we specified process.env to access environment variables, but we have not yet created this file. So we need to do that now.

- Create a file in your Todo directory and name it .env.

`touch .env`

![.env File Output](./image/.env-file-output.PNG)

`vi .env`

![Vi File Output](./image/vi-env-output.PNG)

- Now we need to update the index.js to reflect the use of .env so that Node.js can connect to the database.

- Simply delete existing content in the file, and update it with the entire code below.

- To do that using vim, follow below steps

- Open the file with vim index.js
- Press esc
- Type :
- Type %d
- Hit ‘Enter’
- The entire content will be deleted, then,

- Press i to enter the insert mode in vim
Now, paste the entire code below in the file

![Vim Index Output](./image/vim-index-output.PNG)

- Start your server using the command:

`node index.js`

![Server Database Output](./image/server-database-success.PNG)

- Dowwnload Postman

- Now open your Postman, create a POST request to the API http://<PublicIP-or-PublicDNS>:5000/api/todos. This request sends a new task to our To-Do list so the application could store it in the database.

- Note: make sure your set header key Content-Type as application/json

[Postman Post URL](http://3.144.164.56:5000/api/todos)

![Postman Post Output](./image/postman-output.PNG)

- Create a GET request to your API on http://<PublicIP-or-PublicDNS>:5000/api/todos. This request retrieves all existing records from out To-do application (backend requests these records from the database and sends it us back as a response to GET request):

[Postman Get URL](http://3.144.164.56:5000/api/todos)

![Postman Get Output](./image/postman-get-output.PNG)

- Delete an existing task from the list – HTTP DELETE request

[Postman Delete URL](http://3.144.164.56:5000/api/todos/636d668d01aaa62e45d0ae3a)

![Postman Delete Output](./image/post-delete-output.PNG)

5. **Frontend creation**

- Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.

- In the same root directory as your backend code, which is the Todo directory, run:

`npx create-react-app client`

![Create React App](./image/react-app-output.PNG)

- Running a React App
Before testing the react app, there are some dependencies that need to be installed.

- Install concurrently. It is used to run more than one command simultaneously from the same terminal window:

`npm install concurrently --save-dev`

![Install Concurrently Save](./image/install-concurrently-save.PNG)

- Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes:

`npm install nodemon --save-dev`

![Nodemon Install Save](./image/nodemon-install-output.PNG)

- In Todo folder open the package.json file. Change the highlighted part of the below screenshot and replace with the code below:

![Packagejson Update Output](./image/packagejson-update-output.PNG)

- Change directory to ‘client’

`cd client`

![Packagejson Update](./image/packagejson-update-output.PNG)

- Open the package.json file

`vi package.json`

![Packagejson Update](./image/packagejson-update-output.PNG)

- The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos

- Now, ensure you are inside the Todo directory, and simply do:

`npm run dev`

![Npm Run Dev](./image/npm-run-dev-output.PNG)

- Launch localhost:

[title](http://18.116.235.188:3000/)

![Npm Run Dev](./image/iplaunch-aft-npm-run-dev.PNG)

- Creating your React Components
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component.
From your Todo directory run:

`cd client`

![Client Cd](./image/cd-client.PNG)

- move to the src directory

`cd src`

- Inside your src folder create another folder called components:

`cd src`

![Components Directory](./image/components-dir.PNG)

- Move into the components directory with:

`cd components`

![Cd Components Directory](./image/cd-components-dir.PNG)

- Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js:

`touch Input.js ListTodo.js Todo.js`

![Create 3 Files](./image/crt-input-listtodo-todo.PNG)

- Open Input.js file:

`vi Input.js`

To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.

Move to the src folder:

`cd ..`

![Cd Src](./image/cd-src.PNG)

- Move to clients folder

`cd ..`

![Cd Clients](./image/cd-client-status.PNG)

- Install Axios:

`npm install axios`

![Npm Install Axios](./image/axios-install-output.PNG)


6. **Frontend creation (continued)**

- Go to ‘components’ directory:

`cd src/components`

![CD to Components Directory](./image/cd-src-components.PNG)

- After that open your ListTodo.js:

`vi ListTodo.js`

- In the ListTodo.js, copy and paste the following code:

![Listtodo Write Output](./image/listtodo-write-output.PNG)

- Then in your Todo.js file you write the following code:

![Todo Write Output](./image/todo-write-output.PNG)

- We need to make little adjustment to our react code. Delete the logo and adjust our App.js to look like this.

- Move to the src folder:

`cd ..`

![Todo Write Output](./image/cd-src-folder.PNG)

- Make sure that you are in the src folder and run:

`vi App.js`

![Appjs Write Output](./image/appjs-write-output.PNG)

- In the src directory open the App.css:

`vi App.css`

- Then paste the following code into App.css:

![Appcss Write Output](./image/appcss-write-output.PNG)

- In the src directory open the index.css:

`vim index.css`

- Copy and paste the code below:

![Indexcss Write Output](./image/indexcss-write-output.PNG)

- Go to the Todo directory:

`cd ../..`

![Indexcss Write Output](./image/cd-todo-directory.PNG)

- When you are in the Todo directory run:

`npm run dev`

[title](http://18.116.235.188:3000/)

![Npm Run Dev Step 6](./image/mytodo-output-success-output.PNG)






