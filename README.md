# Proxy-Server
CCBD_BootCamp Task-1

Team Members :
Rohan B Sahu         01FB16ECS305
Prakhyat G Kulkarni  01FB16ECS263
Raghav R Bongole     01FB16ECS286 

Aim:

To build a proxy web-site that serves out web pages of an IPL match and cache
the webpage.
 
Introduction:

Proxy Servers help in implementing Internet access control like authentication
for Internet connection, bandwidth control, Internet web filter and content 
filter etc.Caching the webpage reduces subsequent loading times.We have used
Squid proxy server for this.

Squid is a caching proxy for the Web supporting HTTP, HTTPS, FTP, and more.
It reduces bandwidth and improves response times by caching and reusing 
frequently-requested web pages. Squid has extensive access controls and makes a
great server accelerator. It runs on most available operating systems, including
Windows and is licensed under the GNU GPL.

Procedure:

We first installed and configered the Squid Proxy Server in one system.It is
through this server that the client system will be accessing the internet from.
Configeration involved ,

1.Setting up the http_port for the server which by default is 3128

2.By default , in squid.conf file , the >>http_access is deny all , so we changed 
  it to >>http_access allow all.

3.We, now had to enable caching capabalities.
    
    i) We created a disk cache directory where all the cached data will be stored.
    >>cache_dir ufs /var/cache/squid 200 16 256
    here, ufs(universal file storage) is the format in which the cached data is 
    stored.
    200 means 200 MB of data can be stored.
    16 256 defines the L1 and L2 cache size , ie. 16KB and 256KB respectively.

    ii) Since we want the cache data to keep getting updated , we configure the
    refresh_pattern.
    refresh_pattern .*\.(jpg|gif|MPEG|png|JPEG): 1440     20%     10080
    
    >>*\.(jpg|gif|MPEG|png|JPEG) means the type of data we have to cache.
    1440 means after 1440 minutes(i.e 1 day) refresh the cache.
    20% means after 20% storage , refresh the cache.

4.Now, we connect the client system to the same network as the proxy server but 
in the proxy setting of the client system , we manually configure it to connect
it to the proxy server by setting up the ip address and the port number.

5.To check whether the squid proxy server is working properly and the data is
getting cached , we check the access.log within squid.
>>tail -f /var/log/squid/access.log
As we click any part of the website , espncricinfo , the log file gets updated
instantaneously.
Also , if we check the directory where the cache is getting stored , it gets
updated.


Since we were running the proxy server is normal OS and not a Server OS , we 
could not do Load Sharing with multiple proxy servers.

We do suggest an alternative to Round-Robin Algorithm which is Weighted Round-Robin
Algorithm in order to work with heavy load.

Weighted Round - Robin :
The classic round - robin algorithm for load balancing attempts to equally
distribute the requests between all servers. That may be inefficient since the 
servers may have different capabilities. Weighted Round-Robin provides an effective
way of focusing on fairly distributing the load amongst available resources. Each
server is assigned a value that signifies the server's performance capability 
relative to other servers in the pool. The load is distributed to the servers in 
the same proportion of the weights assigned. In other words, more requests are 
served by a server with a greater weight and fewer requests by a server with a 
lesser weight.

Further, Caching and Load Balancing can be made more robust by using Linux router
utilising multiple uplink providers. With this, we are not only dependent on 1 
internet provider but we make the caching process more fast.

