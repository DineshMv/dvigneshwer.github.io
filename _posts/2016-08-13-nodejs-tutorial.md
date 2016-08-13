---
layout: post
title: "NodeJs : End to end guide"
date: 2016-08-13
---

Node.js is an open source, cross-platform runtime environment for developing server-side and networking applications. 

All APIs of Node.js library are asynchronous that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data.

Node.js uses a single threaded model with event looping.

Installation:
<strong>
sudo apt-get install nodejs

Add /usr/local/nodejs/bin to the PATH environment variable.

export PATH=$PATH:/usr/local/nodejs/bin
</strong>
Check:

nano main.js

console.log("Hello world")

node main.js

If all goes good, then you should see Hello world in the terminal

Things to do :

Import required modules − We use require directive to load a Node.js module.

Create server − A server which will listen to client's request similar to Apache HTTP Server.

Read request and return response − server created in earlier step will read HTTP request made by client which can be a browser or console and return the response.
<strong>
var http = require("http");

http.createServer(function (request, response) {

   // Send the HTTP header 
   // HTTP Status: 200 : OK
   // Content Type: text/plain
   response.writeHead(200, {'Content-Type': 'text/plain'});
   
   // Send the response body as "Hello World"
   response.end('Hello World\n');
}).listen(5000);

// Console will print the message
console.log('Server running at http://127.0.0.1:5000/')
</strong>

saves this in to server.js and run node server.js, open your browser and type 127.0.0.1:5000, you should see Hello World yipee you have stup your http server

Node Package Manager (npm) helps you install node modules
<strong>
npm -version
sudo npm install npm -g // to upgrage

npm install express

var express = require('express'); // to use express in node app

npm ls //shows the package installed locally

npm install express -g // installs in the usr/lib/node-modules location

npm uninstall package_name

npm search module_name
</strong>
Above are few npm commands





