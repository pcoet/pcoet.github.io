---
title: Create a Node.js web service using Express and MongoDB
category: MongoDB
---

In this post, we'll walk through the process of creating a Node.js web service using Express and MongoDB. Our service will support a record store that sells new and used vinyl records. We'll need to handle basic CRUD operations on the inventory - adding a new album, searching for albums, updating an album, and deleting an album. When we're finished, we'll have a simple RESTful API that could support a web application or other client.

Note that our service is only intended for learning purposes. Some of the code and configuration may not be appropriate for a production service.

Okay, let's get started!

## Install MongoDB

First we need to install MongoDB. The installation process varies by operating system. To install MongoDB, go to [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) and follow the instructions for your platform.

After you have MongoDB installed, you'll need to create a **/data/db** directory where MongoDB can write data, and then you can start the server.

1. Create the **/data/db** directory: `sudo mkdir -p /data/db`
1. Make yourself the owner of the directory, so that MongoDB will have permission write to it: `sudo chown -R $USER /data/db`
1. Open a new terminal and run: `mongod`

There are various ways to start and stop the MongoDB server. To learn more about options for running MongoDB, see [Run MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/#run-mongodb) and [Manage mongod Processes](https://docs.mongodb.com/manual/tutorial/manage-mongodb-processes/).

If everything is working as expected, you should see initilization messages logged to the terminal. One of them should look something like this, 

    2019-12-04T10:01:50.471-0800 I  NETWORK  [initandlisten] waiting for connections on port 27017

So MongoDB should be listening for connections on port 27017.

## Create a Node.js application

Now we'll create a Node.js application, which will eventually become our Express service.

If you don't already have Node.js installed, you can [download it](https://nodejs.org/en/download/) or [install it by package manager](https://nodejs.org/en/download/package-manager/). Then we can create a simple Node.js app.

1. Create a new directory for your project: `mkdir record-service && cd record-service`
1. Initialize an NPM project: `npm init -y`
1. In the root directory, create an **app.js** file and add the following code:

   ```javascript
   var hello = 'hello world';
   console.log(hello);
   ```

1. Open **package.json** and alter it to look like this:

   ```javascript
   {
     "name": "record-service",
     "version": "1.0.0",
     "main": "app.js",
     "scripts": {
       "start": "node app.js"
     }
   }
   ```
We've removed a few properties that we don't need, pointed `"main"` at our **app.js** file, and added a `"start"` script tha runs our app. Now let's try it:

    npm start

Your app should output `hello world` to the terminal.

## Build out the Express routes

Now we're ready to build the Express app. First, let's install Express: `npm install express --save`. Then update **app.js** so that it looks like this:

```javascript

```

