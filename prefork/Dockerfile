FROM rockylinux:8.8

RUN dnf -y upgrade && dnf -y module install httpd && dnf -y module install php:7.4
RUN mv /etc/httpd/conf.d/ssl.conf /etc/httpd/conf.d/ssl.conf_ORG
RUN echo "ServerName localhost:80" >> /etc/httpd/conf/httpd.conf
COPY  prefork/startserv.sh /root
RUN   chmod 755 /root/startserv.sh
RUN yum -y install php
RUN sed -i 's/#LoadModule mpm_prefork_module/LoadModule mpm_prefork_module/' /etc/httpd/conf.modules.d/00-mpm.conf && sed -i 's/^LoadModule mpm_event_module/#LoadModule mpm_event_module/' /etc/httpd/conf.modules.d/00-mpm.conf
COPY src/test.php /var/www/html

EXPOSE 80

CMD ["/bin/bash","/root/startserv.sh"]