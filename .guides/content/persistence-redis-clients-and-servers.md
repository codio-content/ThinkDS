Redis is usually run as a remote service; in fact, the name stands for “REmote DIctionary Server”. To use Redis, you have to run the Redis server somewhere and then connect to it using a Redis client. There are many ways to set up a server and many clients you could use. For this exercise, I recommend:



1.  Rather than install and run the server yourself, consider using a service like RedisToGo ([http://thinkdast.com/redistogo](http://thinkdast.com/redistogo)), which runs Redis in the cloud. They offer a free plan with enough resources for the exercise.
1.  For the client I recommend Jedis, which is a Java library that provides classes and methods for working with Redis. 


Here are more detailed instructions to help you get started:



*  Create an account on RedisToGo, at [http://thinkdast.com/redissign](http://thinkdast.com/redissign), and select the plan you want (probably the free plan to get started).
*  Create an “instance”, which is a virtual machine running the Redis server. If you click on the “Instances” tab, you should see your new instance, identified by a host name and a port number. For example, I have an instance named “dory-10534”.
*  Click on the instance name to get the configuration page. Make a note of the URL near the top of the page, which looks like this: ```code redis://redistogo:1234567feedfacebeefa1e1234567@dory.redistogo.com:10534 ``` 


This URL contains the server's host name, `dory.redistogo.com`, the port number, `10534`, and the password you will need to connect to the server, which is the long string of letters and numbers in the middle. You will need this information for the next step.