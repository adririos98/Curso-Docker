FROM centos
RUN sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-* 
RUN sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*
RUN yum -y update 
RUN yum -y install httpd
EXPOSE 80
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]