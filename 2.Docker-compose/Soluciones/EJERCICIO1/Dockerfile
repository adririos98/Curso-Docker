FROM centos
RUN yum -y update && sudo sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-* && sudo sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*
RUN yum -y install httpd
EXPOSE 80
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]