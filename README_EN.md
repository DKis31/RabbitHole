
### Project Rabbithole  

Project Rabbithole is a hobby project for making websites discoverable over one another and providing HTTP tunneling services with a custom HTTP method and a response code.  
##

#### Discovering websites with Greetings
The point of greetings isn't for websites to "keep in touch" with one another but to request for other affiliated websites. One would initiate the conversation with asking for websites and the other would end it after responding.
##
##### The HELLO HI Syntax

The way a HELLO request method should be structured is:

>      HELLO <request-target>["?"<query>] HTTP/1.1
Followed by headers and a body after them.  
>      <request>["?"<query>] 
Is a way to      
The body is a simple JSON file containing an element 'known' which is an array of known IPs and domains in the form of strings.  

##### How does this differ from the GET request method?

Traditionaly the GET request method doesn't have a body. From my research there isn't a request method which:  
* has a body  
* retrieves data
* is safe (doesn't alter the state of the server)
##
#### Affiliations
Affiliations are realised with HTTP tunneling over requested url paths.  
The server should have the ability to send HELLO requests without additional values after the url to the client which would give back a simple HI response.
##
