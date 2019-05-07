## DNS Load Balancing
  If we having multiple instance of same application, then we can do DNS loading balancing to contact any one of them.
### Round Robin
  Whenever the client asks for the application IP to the DNS server, it will give the IPs in random order each time. As it is random(mostly Round Robin), the load is equally balanced to each instance

### VirtualIP
  Whenever the client asks for the application IP to the DNS server, it will give the Virtual IP and on hitting the Virtual IP, it will get redirected any one of the instance IP and thus the load is balanced equally. This is achieved using IP tables and IPVS.

### Problems with Round Robin
  As the DNS server is already doing the ordering, clients should not order the IPs. Ordering will make the imbalance loading [here](https://gist.github.com/SpComb/c509bd064bc75151e6b41e8bc949d13f)

### Reference
- https://sreeninet.wordpress.com/2016/07/29/service-discovery-and-load-balancing-internals-in-docker-1-12/
- https://medium.com/@lherrera/poor-mans-load-balancing-with-docker-2be014983e5