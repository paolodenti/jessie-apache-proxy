# Supported tags and respective Dockerfile links

* `8.7`, `latest` [Dockerfile](https://github.com/paolodenti/debian-apache-proxy/blob/master/Dockerfile)

# Description

Apache 2.4 with proxy (http/html) enabled on Debian Jessie
Ready for single site (can be modified for NameVirtualHost as usual adding .conf in /etc/apache2/sites-enabled)
Original default site has been fully disabled, every request is proxied.

PROXY_HOST: proxied hostname, default 127.0.0.1
PROXY_PORT: proxied port, default 8080

Only port 80 is exposed

e.g. in order to proxy a tomcat running on port 8080 having name "tomcat"
docker run -p 80:80/tcp --env PROXY_HOST=tomcat --env PROXY_PORT=8080 -t paolodenti/debian-apache-proxy

Apache proxy directives internally used are:

ProxyPass / http://${PROXY_HOST}:${PROXY_PORT}/
<Location />
	ProxyPassReverse http://${PROXY_HOST}:${PROXY_PORT}/
</Location>
