FROM mysql:5.7

RUN touch /var/log/mysql/mysqld.log 

ADD ./my.cnf /etc/mysql/my.cnf
RUN chmod 644 /etc/mysql/my.cnf
