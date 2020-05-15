FROM mysql:5.7

# set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN echo "max_allowed_packet=1024M" >>/etc/mysql/mysql.conf.d/mysqld.cnf
RUN echo "sql-mode=""" >>/etc/mysql/mysql.conf.d/mysqld.cnf
RUN mkdir sql