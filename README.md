# wsmschatapp

In our application we have a chat module, by using this chat module the customer can ask their doubts/queries and get them solved. For developing the chat module we have used the socket programming. Both client module and server module are hosted on different servers.

![GitHub Logo](https://github.com/shubhamrajput0369/wsmschatapp/blob/main/wsmschatappinterface.png)

In our application we have used Client Server Architecture.
The Client-server model is a distributed application structure that partitions tasks or workload between the providers of a resource or service, called servers, and service requesters called clients. In the client-server architecture, when the client computer sends a request for data to the server through the internet, the server accepts the requested process and delivers the data packets requested back to the client. Clients (remote processors) request and receive service from a centralized server (host computer).

Client computers provide an interface to allow a computer user to request services of the server and to display the results the server returns. Servers wait for requests to arrive from clients and then respond to them. Ideally, a server provides a standardized transparent interface to clients so that clients need not be aware of the specifics of the system (i.e., the hardware and software) that is providing the service. Clients are often situated at workstations or on personal computers, while servers are located elsewhere on the network, usually on more powerful machines.

How browser interacts with the server:
User enters the URL(Uniform Resource Locator) of the website or file. The Browser then requests the DNS(DOMAIN NAME SYSTEM) Server.
DNS Server lookup for the address of the WEB Server.
DNS Server responds with the IP address of the WEB Server.
Browser sends over an HTTP/HTTPS request to WEB Server’s IP (provided by DNS server).
Server sends over the necessary files of the website.
Browser then renders the files and the website is displayed. 

Advantages of Client-Server Architecture:
Centralized system with all data in a single place.
Cost efficient requires less maintenance cost and Data recovery is possible.
The capacity of the Client and Servers can be changed separately.

In our application we have a chat module, by using this chat module the customer can ask their doubts/queries and get them solved. For developing the chat module we have used the socket programming. Both client module and server module are hosted on different servers.

B) Web-Socket in NodeJS:
Web Socket is a protocol which provides a full duplex(multiway) communication i.e allows communication in both directions simultaneously.
It is a modern web technology in which there is a continuous connection between the user’s browser(client) and the server. In this type of communication, between the web server and the web browser, both of them can send messages to each other at any point in time. 
Traditionally on the web, we had a request/response format where a user sends an HTTP request and the server responds to that. This is still applicable in most of the cases, especially those using RESTful API. But a need was felt for the server to also communicate with the client, without getting polled(or requested) by the client. The server in itself should be able to send information to the client or the browser. This is where Web Socket comes into the picture.
Socket.IO is a JavaScript library for real-time web applications. It enables real-time, bi-directional communication between web clients and servers. It has two parts: a client-side library that runs in the browser, and a server-side library for node.js. Both components have an identical API.

Using express & socket.io:
In order to make use of the Socket in NodeJS, we first need to install a dependency that is socket.io. We can simply install it by running below command in cmd and then add this dependency to your server-side javascript file also install an express module which is basically required for server-side application

npm install socket.io --save

npm install express --save

Create server in your server side javascript file:
const express = require('express'); // using express
const socketIO = require('socket.io');
const http = require('http') 
const port = process.env.PORT||3000 // setting the port 
let app = express();
let server = http.createServer(app)
let io = socketIO(server)
server.listen(port);

Now we need to make a connection from the server side to the client side through which the server will be able to send data to the client.

// make a connection with the user from server side
io.on('connection', (socket)=>{
  console.log('New user connected');
});

Similarly, from the client side, we need to add a script file and then make a connection to a server through which the user sends data to a server.
<script src="/socket.io/socket.io.js"></script>
<script>
var socket=io()
// make connection with server from user side
socket.on('connect', function(){
  console.log('Connected to Server')
});
</script>
 
Now to send messages or data from a server to the user we generate a socket “socket.on()” inside the connection that we made from the server side.

// listener when server emit any message
socket.on('createMessage', (newMessage)=>{
    console.log('newMessage', newMessage);
  })

Now either data can be sent from any side so that a connection is generated between server and client. Then if the server emits a message then the client can listen to that message or if the client emits a message then the server can listen to that message. So we have to generate a socket for both messages emit and message listen on both the server and the client side.
