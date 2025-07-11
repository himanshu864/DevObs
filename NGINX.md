#nodejs 

Powerful web server and uses non-threaded, event-driven architecture.
It can also **load balance**, **HTTP cache**, and can be used as **reverse Proxy.**
## Forward Proxy

![[Pasted image 20240724004643.png]]
A forward proxy is an intermediary that sits between one or more user devices and the internet. Instead of validating a client request and sending it directly to a web server, a forward proxy server evaluates the request, takes any needed actions, and routes the request to the destination on the client’s behalf.

Like VPN. Handles many users, but only one server.

## Reverse Proxy

![[Pasted image 20240724005003.png]]
User don't directly communicate with the server. Nginx decides what action to take, and which server to choose to resolve client's request.

Can handle 10,000 Concurrent Requests.

**Load Balancing**: If a large website or other web service uses multiple origin servers, a reverse proxy can distribute requests among them to ensure even server loads..

**HTTP Caching**: A reverse proxy can cache content from an origin server in temporary storage, and then send the content to clients that request it without further transacting with the server (this is called web acceleration). DNS can be used to route requests evenly among multiple reverse proxies.

**API Gateway**: Can redirect to different servers based on routes.

**SSL Certification**: Can even do this.

# Installation and Setup
---

- We'll install nginx on Docker container.
```bash
docker run -it -p 8080:80 ubuntu
```

By default nginx runs on port 80

- Install nginx and run it.
```bash
apt-get update
apt-get upgrade

apt-get install nginx
nginx
```
Check localhost:8080 on your machine.

- Installation done. Let's configure!
```bash
cd etc/nginx/
mv nginx.conf nginx-backup.config #create backup

apt-install vim
vim nginx.conf # create and edit new config file
```

- *nginx.conf*
```nginx
events {

}

http {
	server {
		listen 80; # listen to port 80
		server_name _; # accept requests from all

		location / { # default home router
			return 200 "Hello from nginx.conf File";
		}
	}
}
```

Now this should be displaying on `localhost:8080/`

## Controlling NGINX
---

To reload your configuration, you can stop or restart NGINX, or send signals to the master process. A signal can be sent by running the `nginx` command (invoking the NGINX executable) with the `-s` argument.

```bash
nginx -s <SIGNAL>
```

where `<SIGNAL>` can be one of the following:

- `quit` – Shut down gracefully (the `SIGQUIT` signal)
- `reload` – Reload the configuration file (the `SIGHUP` signal)
- `reopen` – Reopen log files (the `SIGUSR1` signal)
- `stop` – Shut down immediately (or fast shutdown, the `SIGTERM` singal)

The `kill` utility can also be used to send a signal directly to the master process.

## Contexts
---

A few top‑level directives, referred to as _contexts_, group together the directives that apply to different traffic types:

- [events] – General connection processing
- [http] – HTTP traffic
- [mail] – Mail traffic
- [stream] – TCP and UDP traffic

Directives placed outside of these contexts are said to be in the _main_ context.

## Root Directory and Index Files with Sample Config
---

The [root] directive specifies the root directory that will be used to search for a file.

If a request ends with a slash, NGINX treats it as a request for a directory and tries to find an index file in the directory. The [index] directive defines the index file’s name (the default value is `index.html`).

```nginx
user nobody; # a directive in the 'main' context

events {
    # configuration of connection processing
}

http {
    # Configuration specific to HTTP and affecting all virtual servers

    server {
		root /www/data;
		
        # configuration of HTTP virtual server 1
        location /one {
            # configuration for processing URIs starting with '/one'
        }
        location /two {
            # configuration for processing URIs starting with '/two'
        }

		# search in media if router ends with mp3/mp4
		location ~ \.(mp3|mp4) {
			root /www/media;
		}
    }

    server {
        # configuration of HTTP virtual server 2
    }
}

stream {
    # Configuration specific to TCP/UDP and affecting all virtual servers
    server {
        # configuration of TCP virtual server 1
    }
}
```

# Serving static Content
---

- Make a directory inside /etc/nginx and create index.html

*/etc/nginx/render/index.html* 
```html
<!DOCTYPE html>
<html lang="en">

<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>Document</title>
</head>

<body>
Hello my name is Himanshu
</body>

</html>
```

And edit nginx.conf to server this html

*/etc/nginx/nginx.conf*
```nginx
events {
}

http {
	#types { # optionally define content-type
	#	text/html html;
	#	text/css css; # nginx not smart enough for this
	#}
	
	include /etc/nginx/mime.types;

	server {
		listen 80;
		server_name _;
		
		root /etc/nginx/render; # path of index.html
	}
}
```

- We can choose not to define content-types and nginx will server as best as it can. But that's no good. And also manually typing all types is also no good.
- So just link the built-in *mime.types* file.

