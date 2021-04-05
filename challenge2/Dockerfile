FROM centos:latest

RUN yum -y install httpd

ADD webserver.tar.gz /var/www/html/

CMD ["-D", "FOREGROUND"]

ENTRYPOINT [ "/usr/sbin/httpd" ]

EXPOSE 80

# From challenge folder, `docker build . -t challenge:2`
# then `docker run -p 8080:80 challenge:2`
