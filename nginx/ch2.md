# 2.1 HTTP Load Balancing

Use NGINX’s HTTP module to load balance over HTTP servers using the upstream block:
```
upstream backend {
  server 10.10.12.45:80 weight=1;
  server app.example.com:80 weight=2;
  server spare.example.com:80 backup;
}
server {
  location / {
    proxy_pass http://backend;
  }
}
```

This configuration balances load across two HTTP servers on port 80, and defines one as a backup, which is used when the two primary servers are unavailable.
The optional weight parameter instructs NGINX to pass twice as many requests to the second server. When not used, the weight parameter defaults to 1.

The HTTP upstream module controls the load balancing for HTTP requests. 
This module defines a pool of destinations—any combination of Unix sockets, IP addresses, and server hostnames, or a mix.
The upstream module also defines how any individual request is assigned to any of the upstream servers.
