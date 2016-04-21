#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for webdevops/php-dev-apache:ubuntu-14.04
#    -- automatically generated  --
#+++++++++++++++++++++++++++++++++++++++

FROM webdevops/php-dev:ubuntu-14.04

MAINTAINER info@webdevops.io
LABEL vendor=WebDevOps.io
LABEL io.webdevops.layout=6
LABEL io.webdevops.version=0.23.0

ENV WEB_DOCUMENT_ROOT  /app
ENV WEB_DOCUMENT_INDEX index.php
ENV WEB_ALIAS_DOMAIN   *.vm

COPY conf/ /opt/docker/

# Install apache
RUN /usr/local/bin/apt-install \
        apache2 \
        apache2-mpm-worker \
        libapache2-mod-fastcgi \
	&& sed -ri ' \
		s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; \
		s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g; \
		' /etc/apache2/apache2.conf \
	&& rm -f /etc/apache2/sites-enabled/* \
	&& a2enmod actions fastcgi ssl rewrite headers \
	&& mkdir -p /var/lock/apache2 \
    && /opt/docker/bin/provision-run.sh webdevops-apache webdevops-php-apache \
    && /opt/docker/bin/bootstrap.sh


EXPOSE 80 443