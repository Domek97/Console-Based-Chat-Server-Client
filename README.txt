FILES:
motd- Contains MOTD for users to access. Is not ever edited inside the program
users- contains user data for logging in. Is not ever edited inside the program

Methods: (All methods are accessed by the client and carried out by the server)
Server.class

-get_message: prints the next motd in the list to the user and prepares the next mods to be accessed. 
	usage: NA

-login: logs the user in by checking to see if their credentials match any user in the file users.txt and will print an error if they are already logged in.
	usage: NA

-logout: logs the user out if they are logged in and prints an error if they are not logged in
	usage: NA

-store_message: If the user is logged in, takes their inut as a new motd. Prints an error if they are not logged in.
	usage: NA

-shutdown: If user calling this command is root user, shuts down the server by closing all sockets/streams and ending the application
	usage: NA

-quit: Prints an acknowledgement message to the user before they close the socket
	usage: NA

Client.class
-get_message: receives Server's output as a MOTD 
	usage: MSGGET

-send: sends a private message to a single person. only works if sender and recipient are both logged in
	usage: SEND recipient

-WHO: sends client a list of users currently logged in and their ip addresses.
	usage: WHO
-login: logs the user in by checking to see if their credentials match any user in the file users.txt and will print an error if they are already logged in.
	usage: LOGIN username password

-logout: logs the user out if they are logged in and prints an error if they are not logged in
	usage: LOGOUT

-store_message: Store Message: Receives Server's output on whether user is logged in or not, then sends output to server for new MOTD
	usage: MSGSTORE <new MOTD>

-shutdown: Receives input from server whether it was successful, then closes all sockets and application
	usage: SHUTDOWN

-quit: Receives input from the server, closes all sockets and ends the application
	usage: QUIT

Known bugs:
 -When closing the server using SHUTDOWN or QUIT the client receives an exception that the stream has closed. This does not affect the process.
 -If user uses backspace without control it creates a character for backspace. Using enough of these can erase the user's namestamp on the server's logs.
 -Inputs to user's client have an extra newline than intended because writeUTF adds the newline as well as the rest of the string.

Sample Output
#> - This is what number command the user has committed to see the relationship between client and server. > is output < is input.

Client.class (second client connects right before LOGIN root root01)
0> java Client 127.0.0.1
0< Connected.
1> Hello!
2> LOGIN
2< Wrong UserID or password
3> LOGIN mary mary01
3< 200 OK
4> my name changed!
5> MSGGET
5< 200 OK
5< There is only one way to happiness and that is to cease worrying about things which are beyond the power of our will.
6> MSGGET
6< 200 OK
6< What you do not want done to yourself, do not do to others.
7> MSGSTORE
7< 200 OK
7< Please input new MOTD to be added.
7> You miss every shot you don't take.
7< 200 OK
8> MSGGET
8< 200 OK
8< The only joy in the world is to begin.
9> MSGGET
9< 200 OK
9< Happiness is not something ready-made. It comes from your own actions.
10> MSGGET
10< 200 OK
10< To be happy, we must not be too concerned with others.
11> MSGGET
11< 200 OK
11< You miss every shot you don't take.
12> SHUTDOWN
12< 402 User not allowed to execute this command.
13> LOGOUT
13< 200 OK
13< 127.0.0.1 has connected to the server.
13< User1: Hi!

14>Hello!
15>SEND john
15<200 OK
   Please type message to target.
16>I have a secret to tell you.
17> LOGIN root root01
17< 200 OK
18> SHUTDOWN
18< 200 OK
Server.class (with two clients connected)

(This is the server printing the default MOTD, so moderators may know what MOTDs are custom.)

0>	There is only one way to happiness and that is to cease worry about things which 	are beyond the power of our will.
	What you do not want done to yourself, do not do to others.
	The only joy in the world is to begin.
	Happiness is not something ready-made. It comes from your own actions.
	To be happy, we must not be too concerned with others.
0< 127.0.0.1 has connected to the server.
1< User0: Hello!
2< User failed to log in.
3< User logged in as mary
4< mary: my name changed!
13< mary logged out.
13< 127.0.0.1 has connected to the server.
16< mary -> john: I have a secret to tell you.
17< User logged in as root
18< root user called SHUTDOWN.
