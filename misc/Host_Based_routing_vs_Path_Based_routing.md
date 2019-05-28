### Host Based routing vs Path Based routing

#### Path Based routing

Based on url path, we will redirect to different service.

Refer sample nginx config. (similar configurations for other proxies)
```bash
server {
    server_name my.service.com

    location /contacts/ {
        proxy_pass  $contactsServiceIP;
    }
    location /payment/ {
        proxy_pass  $paymentServiceIP;
    }
}

# my.service.com/contacts will redirect contactsServiceIP
# my.service.com/payments will redirect paymentServiceIP
```

#### Host Based routing

Based on host name, we will redirect to different service. For same ip, we will have multiple hosts.
That means multiple entries in domain server with same value and different key.

> Example: my.service.com and my.service.in points to 35.100.132.100 in dns server

```bash
server {
    server_name my.service.com

    location /contacts/ {
        proxy_pass  $contactsServiceIP;
    }
    location /payment/ {
        proxy_pass  $paymentServiceIP;
    }
}

server {
    server_name my.service.in

    location /contacts/ {
        proxy_pass  $differentContactsServiceIP;
    }
}

# my.service.com/contacts will redirect contactsServiceIP
# my.service.com/payments will redirect paymentServiceIP
# my.service.in/contacts will redirect differentContactsServiceIP
```

If you want to test this in your local,

- run in the proxy server in your localhost
- add entries in `/etc/hosts` as
   ```bash
   127.0.0.1 my.service.com
   127.0.0.1 my.service.in
   ```

Google is using HOST based routing
```
 IP=$(dig +short www.google.com) curl $IP # 301 Moved
 IP=$(dig +short www.google.com) curl $IP -H "Host: www.google.com" # 200 response

```
