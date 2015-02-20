By: Rohit Kapoor - rohit_kapoor@outlook.com

How to transfer a file:

1) The whole project is divided into 5 parts:
	a) Client (ftpc) - reads the file sends to TCPD (Client)
	b) TCPD (Client) - receives data from ftpc and forwards to troll
	c) Troll - receives data from TCPD (Client) and forwards it to TCPD (Server). Can also modify, delay or drop the packet
	d) TCPD (Server) - receives data from troll and sends to ftps.
	e) Server (ftps) - receives data from TCPD (Server) and stores file to disk
2) Client part and troll are in the directory Client and Server part is in the directory Server. 
3) There is a Makefile in the default directory which compiles all the file required at once.
4) To compile all the files go to directory "Homework_2” and type "make".
5) Steps to send a file from Client to Server:
	a) Start the TCPD (Server) by going to Server directory and starting “tcpd <local-port>”. This will start the TCPD (server) at specified port number.
	b) Start the Server (ftps) by starting “ftps <local-port> <tcpd-port>”, where local-port is the port at which server runs and <tcpd-port> is the port where TCPD (Server) is running. This will register the server with TCPD and TCPD will now forward all packets to the server.
	c) Go to Client directory and start Troll by starting “troll <port-number”. This will start troll at the port number specified.
	d) Start the TCPD (Client) by starting “tcpd <local-port> <troll-port>”, where local-port is the port at which TCPD runs and <troll-port> is the port where Troll is running.
	e) Next, start the file transfer by starting the Client by starting “ftp <remote-IP> <remote-port> <local-file> <tcpd-port>”, where remote-IP is the IP of Server and remote-port is the port number of TCPD (Server) and local-file is the file you want to send and tcpd-port is the port of TCPD (Client). 
6) Server will then accept the connection and receive the file and then exit after saving it in the Server directory.
7) You can confirm the file is transferred successfully by checking the "diff" of local file and file received inside the server directory.
8) For sending the next file, just kill TCPD (server) and do steps (a), (b) and (e) again.