---
layout: post
title: Chatter System
description: "This set of applications was created as a UIS CSC583 network programming term project in the fall of 2015. It includes a chatter server and a chatter client, and provides instant messaging services over the local area network. The chatter server application is command line based, and runs on a vacant port of its host computer. The chatter client is a graphical user interface based application that allows communication through the chatter server to other clients on a local area network. Each client connects to the server, and the server broadcasts incoming messages from a client to all other connected clients. The server has the capability of maintaining a list of users who have previously connected to the system in a MySQL database."
modified: 2015-11-29
tags: [desktop, java]
comments: false
image:
  feature: desktop/chattersystem-banner.png
---

## UIS CSC583 Network Programming Term Project (Fall 2015)

Considering that future classes may require the same term project, I will not provide the source code. Instead, I will provide a summary of the project, along with download links to the completed jar files (should anyone want to run the application).

This set of applications includes both a [chatter server]({{ site.url }}/downloads/chattersystem/ChatterServer.jar) and a [chatter client]({{ site.url }}/downloads/chattersystem/ChatterClient.jar), and provides instant messaging services over the local area network. The chatter server application is command line based, and runs on a vacant port of its host computer. The chatter client is a graphical user interface based application that allows communication through the chatter server to other clients on a local area network. Each client connects to the server, and the server broadcasts incoming messages from a client to all other connected clients. The server has the capability of maintaining a list of users who have previously connected to the system in a MySQL database.

Feel free to download the [chatter server]({{ site.url }}/downloads/chattersystem/ChatterServer.jar) and [chatter client]({{ site.url }}/downloads/chattersystem/ChatterClient.jar) jar applications.

## Application Features

#### <u>Multi-Cast DNS with the JmDNS Library:</u>
[JmDNS](http://jmdns.sourceforge.net) is a Multi-Cast DNS implementation for Java used for service registration and discovery, allowing for automated service discovery. This feature was added to simplify the client/server connection. There is no need to manually find and enter the IP address, or hard code a port number within the desktop or client applications.

#### <u>Links to MySQL to Store Client Names:</u>

The server stores the display names of previously connected clients in a MySQL database, using the client's IP address as a lookup value. When a client first connects, the server queries the database to determine if that client has an established display name. If not, the server requests that the client provides a display name prior to letting that client enter the discussion.

#### <u>Multithreaded:</u>

The chatter server is a multithreaded application that uses a ServerSocket to accept incoming client connections. Once a client connects, the server spawns a new thread specifically for that client. The server maintains a synchronized linked list of all connected clients, which is used to broadcast messages.

## The ChatterServer Java Desktop Application

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/chatterserver.png" alt="">
</figure>

#### <u>Basic Functionality:</u>

The chatter server has the ability to connect to a MySQL database via Connector/J, the official JDBC driver for MySQL, to maintain a list of clients that have accessed the service. The server application includes an option to disable the use of MySQL. When the server is started, it creates a server socket on an open port and uses multi-cast DNS to broadcast the server’s IP address and port number over UDP on the local area network, greatly reducing the configuration requirements of the client. When a client connects to the server, the database is queried (if MySQL is enabled) to determine if the client’s IP address is associated with a username. If the username is found in the database, a message is broadcast to all attached clients that the user has joined the discussion. If the user is not found, the server sends a message to the client requesting the username. When the server receives a message from a client, it broadcasts the client’s name, along with the client’s message, to all connected clients. If the server receives a “Bye” message from a client, it broadcasts that the client has left the discussion before closing the connection with that client.

#### <u>Setting up the database:</u>

The Chatter Server application uses a MySQL database that must be created prior to running the application. This database can have any chosen name. To create this database, start MySQL and enter the query, “CREATE DATABASE database_name;” (where database_name is replaced with the chosen name of the database).

Once the database is created, a database administrator with full privileges to that database is required for the Chatter Server application to perform the necessary queries. After creating the database, issue the following queries:

* “USE database_name;”
* “CREATE USER ‘administrator_name’@’localhost’ IDENTIFIED BY ‘password’;”
* GRANT ALL PRIVILEGES ON database_name.* TO ‘administrator_name’@’localhost’;

administrator_name should be replaced with the name of the database administrator, database_name should be replaced with the chosen name of your database, and password should be replaced with the unique password for the administrator.

You are now ready to run the server.

#### <u>Running the Server:</u>

Open a command prompt or terminal at the location of the ChatterServer.jar file, and enter, "java -jar ChatterServer.jar". Follow the prompts for enabling or disabling MySQL. The server is running and ready to accept client connections when the console states "JmDNS service is registered". There is no need to configure an IP address or port number. The server selects a random port number, and uses the multi-cast functionality of JmDNS to broadcast its IP address and port number over the local area network.

#### <u>External Libraries:</u>

The chatter server application uses the official JDBC driver for MySQL, Connector/J, to connect to the MySQL database. This external package is freely available on [MySQL.com]( http://dev.mysql.com/downloads/connector/j/).

The server also uses the multi-cast functionality of the JmDNS external package to broadcast its location on the local area network. The JmDNS package is freely available and can be downloaded from [sourceforge](http://sourceforge.net/projects/jmdns/).

## The ChatterClient Java Desktop Application

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/chatterclient.png" alt="">
</figure>

#### <u>Basic Functionality:</u>

The chatter client is a graphical user interface based application that connects the user to other clients through the chatter server. The client uses DNS service discovery to automatically detect a running chatter server on the local area network, eliminating the need for IP address and port number configuration. When a client initially connects to a discovered chatter server, the server requests the client’s username, and a message is broadcast to all connected clients that the user has joined the discussion. Any message the client sends to the server thereafter is broadcasted, along with the client’s username, to all connected clients. To leave the discussion, the client sends the message, “Bye”, to the server.

#### <u>Running the Client:</u>  

To run the Chatter Client, simply double click the ChatterClient.jar file. You can also run the client by opening a command prompt or terminal at the ChatterClient.jar location and entering, "java -jar ChatterClient.jar".

When the Chatter Client application is first opened, it begins searching for a running Chatter Server. This search is automatic, requiring no IP address or port number configuration within the client. A message is displayed while the Chatter Client searches for the Chatter Server, and the Send button, used to send messages to the server, is disabled until a connection is made.

When the Client connects to the server for the first time, the server will request the client to supply a display name. Enter a display name in the popup box, and select “OK”.

Once the display name is set, or if this is not the first time this client has connected to the server, a message is displayed welcoming you to the Chatter system with instructions for exiting the discussion. The “Send” button is enabled, and the Chatter server broadcasts a message to all connected clients that you have entered the discussion. You’re ready to start chatting.

To send a message, enter the message you wish to send into the text box at the bottom left side of the screen, next to the send button, and press the send button. The message is then broadcast to all connected clients.

To change your display name, select "Change Name" from the file menu.

You may exit the discussion in one of three ways: selecting the "Exit" option from the file menu, closing the chatter client window, or sending the message, "Bye".

#### <u>External Libraries:</u>

The chatter client application uses the DNS service discovery functionality of the JmDNS external package to discover a running chatter server on the local area network. The JmDNS package is freely available and can be downloaded from [sourceforge](http://sourceforge.net/projects/jmdns/).


## Conclusion

This was an extremely fun project that strengthened my skills in three specific areas:

* Multithreading - The server spawns a new thread for each connected client.
* Multi-cast DNS - Using Multi-cast DNS and DNS-SD through the JmDNS library allowed for a greatly simplified network connection process. With this method, there is no need to manually determine IP addresses or to hard code port numbers.
* MySQL and JDBC - The server interacts with a MySQL database to store client display names.

If I had more time, there are a few features I would have liked to include. First, I would have added encryption to ensure only the connected clients could read the discussion. Second, I would have used XML to standardize the messages to simplify the creation of different client types (e.g. mobile app clients). Third, the use of a full MySQL database is overkill for storing client names. I would have expanded the database to store full conversations. Finally, I would have added the ability for private conversations.
