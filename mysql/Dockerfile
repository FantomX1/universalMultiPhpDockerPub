#FROM mysql:5.6

#FROM library/debian

FROM openshift/mysql-56-centos7

USER root
#RUN yum  update && yum  install sudo  -y

#RUN apt-get update && apt-get install mysql-server -y


#RUN rm -Rf /var/lib/mysql

#RUN sudo  chmod  -R 0777  /home

#RUN   chmod  -R 0777  /var/lib

RUN   chmod  -R 0777  /var/lib/mysql

RUN rm -rf /var/lib/mysql/ibdata1

#RUN   chmod  -R 0777  /var/lib/mysql


#RUN sudo umount /var/lib/mysql

#RUN sudo  ls -la /var/lib/mysql/



# MYSQL_DATABASE=<schema_name> \
ENV MYSQL_ROOT_PASSWORD=root \
    MYSQL_USER=admin \
    MYSQL_PASSWORD=123

ADD . /docker-entrypoint-initdb.d

RUN   chmod  -R 0777  ./docker-entrypoint-initdb.d

RUN ls -la docker-entrypoint-initdb.d

#CMD --sql_mode=""

#EXPOSE 3306

RUN  ls -la /var/lib 

RUN ls -la && cat /etc/passwd

#RUN chmod -R 0777 /var/run

#CMD   /etc/init.d/mysql start  && tail -f /dev/null

USER 1000030000
