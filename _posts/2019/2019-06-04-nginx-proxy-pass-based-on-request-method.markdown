---
title: "Nginx proxy_pass Based on Request Method"
date: "2019-06-04 11:04"
categories: nginx
---

We may want to forward the requests to different upstreams based on the request method. E.g,
* Forward write requests to write upstreams
* Forward read request to read upstreams

Here is an example configuration.
```nginx
upstream read {
  server server1;
  server server2;
}

upstream write {
  server server3;
  server server4;
}

server {
  # Some other configurations
  location / {
    proxy_pass http://read
    limit_except GET {
      # for method is not 'GET', such as PUT, POST will be forward to write upstream
      proxy_pass http://write
    }
  }
}
```
