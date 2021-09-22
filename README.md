# Network-Sockets-with-TCP

A simple program demonstrating Unicast TCP network in Java.

TCP protocol processes run on different machines and communicate with each other by sending messages into sockets. Each process is analogous to a ‘house’ and the process’s socket is analogous to a ‘door’. As shown in the diagram below, the ‘socket’ is the ‘door’ between the application process and TCP.

![Screenshot 2021-09-22 at 20 35 44](https://user-images.githubusercontent.com/58150120/134410093-a40314d8-9511-4800-b975-eae3c5c8372f.png)

### How the connection is initiated?

1. The server has to be running a process, and listening for the client
2. The server must have some sort of ‘door’ - a socket that accepts some initial contact from a client process running on the host
3. The client has the job of initiating the connection with the server

### How do the server and client communicate? 

If the server process is running, then the client can initiate a TCP connection to the server. This happens as follows:

1. The client creates a ‘socket’ and specifies the address of the server process, which is: IP address of the server and the port number of the server process.
2. When the ‘socket’ has been created in the client program, TCP in the client then initiates a three-way handshake and establishes a TCP connection with the server.
3. The three-way handshake takes place at the transport-layer and is completely transparent to the server and client programs.

During the three-way handshake the client knocks on the ‘door’ of the server process requesting a connection. The server responds by opening the ‘door’ - i.e. creating a new socket, which is dedicated to that particular client. At the end of the handshaking phase, a TCP connection exists between the client’s socket and the server's new socket, referred to as the server’s ‘connection socket’. There now exists a direct virtual pipe between the client’s socket and the server's connection socket.

## Starting the Server and Client

The server needs to be running first so it can be waiting for the client to connect (‘knock on the door’) to the server and commence the ‘three-way handshake’ to establish the connection, ready for communication to begin. To run the server, type the following command in the command/terminal window: "java ServerSide".

The server is now running - waiting and listening for the client’s request to connect. When the client connects, the link is established and communication can begin.

To run the client you have to type in the command "java ClientProgram", press Enter and you will see the message  “Connected to server - pipe open” in the client window and “Client accepted" in the server window.

The connection is now established and communication can begin. As this is a unicast simplex TCP socket connection the communication is only one-way - from the client to the server and continues as long as the connection is maintained.

![Screenshot 2021-09-22 at 20 50 50](https://user-images.githubusercontent.com/58150120/134412151-ceb63a20-24c9-4db0-867d-340e8b0d4acd.png)

If you type a message in the client command window you will see it echoed in the server window

![Screenshot 2021-09-22 at 20 51 15](https://user-images.githubusercontent.com/58150120/134412197-845e6423-6850-4b54-997b-58eff7749058.png)

## Analysing TCP connection using Wireshark 

Our connection is running locally on what’s known as the loopback with an IP address of 127.0.0.1. To monitor our connection you need to double-click on Loopback lo0 and the packet capture will begin. You will see quite a bit of traffic on the loopback as it is used for system processes.  With Wireshark running, send a message and Wireshark will capture the process and show the details. When you have sent the message you should immediately press the red "stop" button on Wireshark (top left next to the blue fin), which will pause the collection of any more data. 

![Screenshot 2021-09-22 at 20 55 26](https://user-images.githubusercontent.com/58150120/134413205-ca0771dd-b967-4458-9c50-8f5899c6b3c0.png)

Your TCP socket will be highlighted lilac and you should look for TCP under the ‘Protocol’ heading and an arrow pointing to or from the socket port 1735. You can see above that the last two lines are my communication that has been captured. The bottom line is the acknowledgement [ACK] and the next line up is the message [PSH]. Its source is the loopback 127.0.0.1 and its protocol is TCP and the ports in use are 64259 and 1735. The communication pipe is the connection to the server and client via port 1735 and the welcoming port is 64259, which completes the ‘three-way handshake’
