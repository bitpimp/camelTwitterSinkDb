camelTwitterSinkDb
==================

Sample Apache Camel project showing consuming of twitter messages into a NoSQL DB  

The integration is showing a twitter search that transforms results into JSON and  
routes them to CouchDB instance.  

Requires an instance of CouchDB and creation of Twitter application via:  
https://dev.twitter.com/apps/ then obtaining the security credentials for API access and using them here.  

Set Twitter and CouchDB configuration in applications.properties, eg:  
```  
search.type=polling  
search.delay=60  
search.keywords=camel  
consumerKey=<obtain from https://dev.twitter.com/apps/>  
consumerSecret=<obtain from https://dev.twitter.com/apps/>  
accessToken=<obtain from https://dev.twitter.com/apps/>  
accessTokenSecret=<obtain from https://dev.twitter.com/apps/>  
url=couchdb:http://localhost/YourDB  
``` 
  
  
=============================  
eg. running it with keywords "game of thrones"  
```
[                          main] MainSupport                    INFO  Apache Camel 2.11.0 starting  
[                          main] DefaultCamelContext            INFO  Apache Camel 2.11.0 (CamelContext: camel-1) is starting  
[                          main] ManagementStrategyFactory      INFO  JMX enabled.  
[                          main] DefaultTypeConverter           INFO  Loaded 177 type converters  
[                          main] CouchDbClientBase              INFO  >> GET / HTTP/1.1  
[                          main] CouchDbClientBase              INFO  << Status: 200  
[                          main] ultManagementLifecycleStrategy INFO  Load performance statistics enabled.  
[                          main] DefaultCamelContext            INFO  Total 1 routes, of which 1 is started.  
[                          main] DefaultCamelContext            INFO  Apache Camel 2.11.0 (CamelContext: camel-1) started in 0.588 seconds  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  ***************************************  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  User: ｔｈｒｉｌｌｈｏ  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  Date: Thu May 30 09:25:42 EST 2013  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  Text: Game of Thrones FAQ http://t.co/Tk3jCMqJLV  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  ***************************************  
[) thread #0 - twitter://search] CouchDbClientBase              INFO  >> PUT /twitter/02d7c82c83cc4d659486c9367ec5cd74 HTTP/1.1  
[) thread #0 - twitter://search] CouchDbClientBase              INFO  << Status: 201  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  ***************************************  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  User: Becky Evans  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  Date: Thu May 30 09:25:37 EST 2013  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  Text: A little late to the game, but I'm officially hooked on Game of Thrones! Can't stop watching #Addicted #SoGood  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  ***************************************  
[) thread #0 - twitter://search] CouchDbClientBase              INFO  >> PUT /twitter/e218f81f34a24ae29c5f89d396435cdf HTTP/1.1  
[) thread #0 - twitter://search] CouchDbClientBase              INFO  << Status: 201  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  ***************************************  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  User: Dewey Carter  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  Date: Thu May 30 09:25:26 EST 2013  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  Text: "8 Business Lessons From Game of Thrones" good read http://t.co/KjrlXNIBnp  
[) thread #0 - twitter://search] MyRouteBuilder                 INFO  ***************************************  
[) thread #0 - twitter://search] CouchDbClientBase              INFO  >> PUT /twitter/fbe979b09f4b42b5863bad9141f4d095 HTTP/1.1  
[) thread #0 - twitter://search] CouchDbClientBase              INFO  << Status: 201  
```


====================   
Example CouchDB JSON doc:  
```
{  
   "_id": "ff5f6613982041558a62ff963d74fc01",  
   "_rev": "1-fe19ab06ad8b1869a43cb9ab6c9857de",  
   "user": "Lawrence Fontana",  
   "timestamp": "Thu May 30 09:41:06 EST 2013",  
   "text": "RT @TomChivers: This might be the best thing ever: cat sings the Game of Thrones theme tune http://t.co/nK6p7cX8i7 via @BuzzFeedUK"  
}  
```
