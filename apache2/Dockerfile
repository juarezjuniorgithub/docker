FROM httpd
COPY ./httpd.conf /usr/local/apache2/conf/httpd.conf
COPY ./*.so /usr/local/apache2/modules/
COPY ./index.html /usr/local/apache2/htdocs/index.html
COPY ./server.crt /usr/local/apache2/conf/server.crt
COPY ./server.key /usr/local/apache2/conf/server.key
COPY ./httpd-ssl.conf /usr/local/apache2/conf/extra/httpd-ssl.conf
COPY ./httpd-ssl.conf /usr/local/apache2/conf/original/extra/httpd-ssl.conf
CMD ["apachectl", "-D", "FOREGROUND"]
