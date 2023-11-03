FROM rockylinux:8.8

RUN dnf -y upgrade && dnf -y module install httpd && dnf -y module install php:7.4
RUN mv /etc/httpd/conf.d/ssl.conf /etc/httpd/conf.d/ssl.conf_ORG
RUN echo "ServerName localhost:80" >> /etc/httpd/conf/httpd.conf
COPY  event/startserv.sh /root
RUN   chmod 755 /root/startserv.sh
RUN dnf -y install php-fpm
RUN mkdir /run/php-fpm
COPY src/test.php /var/www/html

EXPOSE 80

CMD ["/bin/bash","/root/startserv.sh"]