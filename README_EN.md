
### Project Rabbithole  

Project Rabbithole is a hobby project for making websites discoverable over one another and providing HTTP tunneling services with custom HTTP requests and responses.  
##

#### Making websites discoverable with Greetings
The point of greetings isn't for websites to "keep in touch" with one another but to request for other affiliated websites. One would initiate the conversation with asking for websites and the other would end it after responding.
##
##### The HELLO HI Syntax

The way a HELLO request should be structured is:
```
HELLO *url\r\n  
KEY *key\r\n  
KNOWN *ip,addr  
```
*There shouldn't actually be additional new line characters after the \r\n it was just added to make the example easier to read. An actual example would look like:

>      HELLO *url\r\nKEY *key\r\n\KNOWN *ip,addr

As you can see the fields are seperated by a carriage return and a new line character after it. This is to make the seperation of fields easier for the greetee (the pair shouldn't be added at the end of the last field) since the values aren't supposed to have special characters, speaking of values:

* *url  
>The request url trailing for the greetee's website. The greetee could want the *url value for deciding which websites' addresses it would return i.e: the greetee getting a *url equal to "/recommended/restaurants" would attach addresses of websites whoose pages are for locations of restaurants, while if it got a *url equal to "/shop/comics" would attach addresses for websites that (you won't guess) sell comics. It is an optional value if the greetee doesn't require it.  
* *key  
>A key the greetee could want for security purposes. It is an optional value if the greetee doesn't require it. Unlike the *url if the value isn't required the entire field should be missing.  

* *ip,addr  
>IPs and url adresses of known websites. This is so the greetee knows whether one of their known websites would be a duplicate if they were to be attached to the response. If the greeter doesn't want to attach addresses '''{}''' should be attached i.e: '''KNOWN {}'''  

The way a HI response should be structured is:
```
HI *msg\r\n\r\n
KNOWN *ip,addr
```

* *msg -> One of these possible types: NOKEY, INVURL, NOKNOWNS, HASKNOWNS.  
>NOKEY -> A message denoting that the greeter didn't attach a correct key value or any key value. The KNOWN field should be entirely missing if this is the *msg type.  
INVURL -> Invalid URL is a message denoting that the greeter didn't attach a correct *url value. The KNOWN field should be entirely missing if this is the *msg type.  
NOKNOWNS -> A message denoting that the greetee didn't attach the KNOWN field. The KNOWN field should be entirely missing if this is the *msg type.  
HASKNOWNS -> A message denoting that the greetee did attach the KNOWN field. The KNOWN field should be found after the '''\r\n\r\n''' sequence.  

* *ip,addr
>Ditto from HELLO
##
#### Affiliations
Affiliations are realised with HTTP tunneling over requested url paths.  
The server should have the ability to send HELLO requests withouth additional values after the url to the client which would give back a simple HI response.
##
##### The Affiliation Request Syntax
The way a JOIN request should be structured is:
```
JOIN *url\r\n
KEY *key\r\n
HEADERS\r\n
```

* *url
>The requested url path which will be for tunnelling HTTP requests to the affiliate client. 
* *key
>Ditto from HELLO
* HEADERS
>Experimental field that is optional, this field should be **at the end**.  

The way a HI response should be structured is:
```
HI *msg\r\n\r\n
```

* *msg -> One of these possible types: NOKEY, INVURL, DENY, ALLOW.  
>I believe types should be self-explanatory.