

Nginx as a load balancer:

Install nginx on three server one for load balancer.

$ sudo apt-get update -y

$ sudo apt-get install -y nginx

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/01\_nginx\_install.png)

$ sudo netstat -tnlp

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/02\_nginx\_listenport.png)

$ /etc/init.d/nginx reload

$ /etc/init.d/nginx reload

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/03\_nginx\_status.png)

$ http://192.168.33.67:80

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/04\_nginx\_browser.png)

$ curl 192.168.33.67

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/05\_content\_index\_curl.png)

configure nginx default file in load balancer server

$ /etc/nginx/sites-available/defaults

# for round robbin (default)

upstream web\_backend {

       server 192.168.33.67;

       server 192.168.33.68;

}

server {

       listen 80;

       location / {

              proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;

              proxy\_pass http://web\_backend;

   }

}

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/07\_nginx\_LB\_default.png)

$ sudo nginx -t

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/08\_nginx\_default\_syntax.png)

$ curl 192.168.1.52

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/11\_req\_LB.png)

![nginx]()

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/09\_req1\_LB.png)

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/10\_req2\_LB.png)

Now configure default file for least-connections: A new request is sent to the server with the fewest current connections to clients.

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/12\_nginx\_default\_least\_conn.png)

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/12\_nginx\_least\_conn\_output.png)

Now configure default file for the ip\_hash :The IP address of the client is used to determine which server receives the request.

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/13\_nginx\_ip\_hash\_default.png)

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/13\_ip\_hash\_output2.png)

Based on weights:

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/14\_nginx\_weighted\_default.png)

![nginx](https://github.com/arunkundrupu1990/nginx/blob/master/images/14\_nginx\_weighted\_output.png)


