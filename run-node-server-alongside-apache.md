# Run A Node App Sever Alongside Apache

This guide shows how to run a Node.js daemon process alongside Apache, with a nice, clean URL.

The best way to build with Node.js is using a dedicated hosting provider, but sometimes you just want to tinker. A node daemon can easlity be run on a different port to Apache, but nobody likes a dirty URL.

# Linux (Ubuntu)

The first step is going to be making sure you have [mod_proxy](http://httpd.apache.org/docs/2.2/mod/mod_proxy.html) and [mod_proxy_http](http://httpd.apache.org/docs/2.0/mod/mod_proxy_http.html) installed. There are [detailed guides](http://abhirama.wordpress.com/2008/11/03/apache-mod_proxy-in-ubuntu/) which should be looked at before following this guide verbatim.

If you're fortunate and the `proxy_http` module is in the `mods-enabled` directory then you might simply have to run:

```
a2enmod proxy_http
```

Otherwise the following steps should be the following...

Install reverse_proxy module:
```
sudo apt-get install libapache2-mod-proxy-html
```

Install libxml if it is not already installed:
```
apt-get install libxml2-dev
```

Load the modules in apache2.conf file (thanks to @kevva for this):
```
sudo a2enmod proxy_module proxy_http_module headers_module deflate_module
```

Now, hopfully you didn't have to pull your hair out tring to those Apache modules. I lost quite a bit of time to it initially, but unfamiliar things always seem to sap the most time.

With the first part behind, we should be good to go adding the following rules to our Apache virtualhost config, which should found in `/etc/apache2/sites-available/your-node-virtualhost-domain.com`

``` xml
<VirtualHost *:80>
	# Admin email, Server Name (domain name), and any aliases
	ServerAdmin your@email.com
	ServerName  www.amazeapp.com
	ServerAlias amazeapp.com

	# Index file and Document Root (where the public files are located)
	DirectoryIndex index.html index.php
	DocumentRoot /var/www/amazeapp.com/public_html

	ProxyRequests off
	<Proxy *>
		Order deny,allow
		Allow from all
	</Proxy>
	<Location />
		ProxyPass http://localhost:3000/
		ProxyPassReverse http://localhost:3000/
	</Location>

	# Log file locations
	LogLevel warn
	ErrorLog  /var/www/amazeapp.com/log/error.log
	CustomLog /var/www/amazeapp.com/log/access.log combined
</VirtualHost>
```

You should only have to add the proxy content. We're telling Apache that every request that comes through the standard port (80) should be routed through our soon to be running node server and its own port (3000).

You'll want to make sure Apache knows the site is available:

```
a2ensite amazeapp.com
service apache2 reload
```

Apache should now be doing its thing, so all that's left it to run our Node app:

```
node /path/to/your/app.js
```

However, if you're connected remotely via ssh, when you log out your `node` process is going to be killed. So we need to make sure the process is run as a daemon process:

```
node /path/to/your/app.js >/dev/null 2>&1 &
```

I'll admit I stumbled upon that command somewhere in Stack Overflow. I can't say it's the most correct way to do it, but it's essentially running the node process silently, outputting no errors, and pushing it to a background task. If we choose to logout a this point it should continue to run as long as there aren't any errors. I would recommend running [Remy Sharp's nodemon](https://github.com/remy/nodemon), but that's your call.

If you've gotten this to work you're more than likely going to want to do it many more times. I [created a gist](https://gist.github.com/adamcbrewer/6060840) just to refer to when I need to set up a new domain virtualhost and run a new background task.


#### References And Links

[Tuts+ - Going Live With Node](http://hub.tutsplus.com/tutorials/going-live-with-node--net-33923)

[Hosting A Node.js Site Through Apache](http://thatextramile.be/blog/2012/01/hosting-a-node-js-site-through-apache)

[mod_proxy](http://httpd.apache.org/docs/2.2/mod/mod_proxy.html)

[mod_proxy_http](http://httpd.apache.org/docs/2.0/mod/mod_proxy_http.html)

[Detailed guide to mod_proxy in Ubuntu](http://abhirama.wordpress.com/2008/11/03/apache-mod_proxy-in-ubuntu/)

[Virtualhost setup along with daemon node task](https://gist.github.com/adamcbrewer/6060840)
