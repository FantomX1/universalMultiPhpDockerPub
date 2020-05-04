#FROM gliderlabs/alpine:3.8
FROM ubuntu:18.04
USER root


RUN  apt update && \
 apt install apache2 libapache2-mod-fcgid -y



RUN apt-get install software-properties-common -y \
&& add-apt-repository ppa:ondrej/php

### to ommit interactive tzdata shell
RUN apt update &&\
    export DEBIAN_FRONTEND=noninteractive && apt install  php5.6 php5.6-fpm -y  &&\
    apt install  php7.0 php7.0-fpm -y &&\
    apt install  php7.1 php7.1-fpm -y &&\
    apt install  php7.2 php7.2-fpm -y


RUN apt-get install curl wget sudo -y

RUN apt-get install vim -y

RUN apt-get install git -y

RUN apt-get install zip unzip -y


# to issuing /sbin/ip route|awk '/default/ { print $3 }' >> php.ini
RUN apt-get install iproute2 unzip -y



### PHP 5.6
RUN apt-get install php5.6-xml -y

RUN apt-get install php5.6-sqlite3 -y

RUN apt install php5.6-zip -y



### PHP 7.0
RUN apt-get install php7.0-xml -y

RUN apt-get install php7.0-sqlite3 -y

RUN apt install php7.0-zip -y


### PHP 7.1
RUN apt-get install php7.1-xml -y

RUN apt-get install php7.1-sqlite3 -y

RUN apt install php7.1-zip -y




### PHP 7.2
RUN apt-get install php7.2-xml -y

RUN apt-get install php7.2-sqlite3 -y

RUN apt install php7.2-zip -y





#&& apt install  php5.6 php5.6-fpm -y
#apt install  php7.2 php7.2-fpm -y

RUN  curl --silent --show-error https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && \
    alias composer='/usr/local/bin/composer.phar'



# yarn must remove cmdtest yarn other app and then add repository update according it and install
RUN apt remove cmdtest \
 && apt remove yarn \
 && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg |  apt-key add - && \
             echo "deb https://dl.yarnpkg.com/debian/ stable main" |  tee /etc/apt/sources.list.d/yarn.list \
 && apt update \
 &&  apt-get install yarn -y


RUN apt install php7.2-mysql php7.1-mysql  php7.0-mysql  php5.6-mysql  -y


RUN apt install php7.2-bcmath php7.1-bcmath  php7.0-bcmath php5.6-bcmath  -y


RUN apt install php7.2-curl php7.1-curl  php7.0-curl php5.6-curl  -y


RUN mkdir /.composer && chmod -R 0777 /.composer



RUN  apt install php-xdebug -y

#RUN  apt install php-xdebug = 2.4.0-1 -y
#RUN  apt install php-xdebug=2.6.0-0ubuntu1 -y was due to old phpstorm bug with xdebug


#RUN apt update &&  apt install 2.6.0-0ubuntu1 -y


RUN apt update && apt install php-memcached -y

RUN  apt  install php-memcache -y

RUN apt install php7.2-ldap  php7.1-ldap php7.0-ldap php5.6-ldap -y

RUN apt update && apt install php7.2-mbstring php7.1-mbstring  php7.0-mbstring php5.6-mbstring -y

RUN apt install php7.2-gd   php7.1-gd   php7.0-gd php5.6-gd -y

RUN apt install make -y

RUN  apt update && apt install php7.2-soap   php7.1-soap php7.0-soap php5.6-soap -y

RUN  apt-get update && apt-get install -y libmemcached11 libmemcachedutil2 build-essential libmemcached-dev libz-dev memcached
#RUN  pecl install memcached-3.0.4
#apt-get install php-pear

RUN echo "nobody:x:999:" >> /etc/groups

# for new change in fpm
RUN echo "nobody:x:999:" >> /etc/group


RUN echo "cd /var/www/html" >> /root/.bashrc


####### INSTALL SECTION

RUN a2enmod actions fcgid alias proxy_fcgi rewrite \
   && mkdir -p /var/www/ \
   && mkdir -p /var/www/html \
   && ln -s /var/www/html /var/www/php56  \
   && ln -s /var/www/html /var/www/php70  \
   && ln -s /var/www/html /var/www/php71  \
   && ln -s /var/www/html /var/www/php72  \
   #&& mkdir -p /var/www/php56 \
   #&& mkdir -p /var/www/php72 \
   && echo "<?php phpinfo(); ?>" > /var/www/html/index.php



RUN rm /etc/apache2/sites-enabled/000-default.conf
RUN echo '' > /etc/apache2/sites-enabled/000-default.conf
RUN echo '' > /etc/apache2/sites-enabled/000-default.conf
COPY   ./php.conf /etc/apache2/sites-enabled/000-default.conf
#COPY   ./php5.6.conf /etc/apache2/sites-available/php56.localhost.conf
#COPY   ./php7.2.conf /etc/apache2/sites-available/php72.localhost.conf
#RUN a2ensite php.localhost

# necesssary to be able to run modes
RUN mkdir -p /var/run/php

#RUN sudo echo "127.0.0.1 php56.localhost" >> /etc/hosts
#RUN sudo echo "127.0.0.1 php72.localhost" >> /etc/hosts



#RUN a2ensite php56.localhost && a2ensite php72.localhost

#RUN  echo 'zend_extension="/usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so"' >> /usr/local/etc/php/php.ini
#RUN  echo 'xdebug.remote_port=9000\' >> /usr/local/etc/php/php.ini
#RUN  echo 'xdebug.remote_enable=1' >> /usr/local/etc/php/php.ini
#RUN  echo 'xdebug.remote_handler=dbgp' >> /usr/local/etc/php/php.ini
## RUN  echo 'xdebug.remote_host=192.168.0.107' >> /usr/local/etc/php/php.ini
##RUN  echo "xdebug.remote_host="`/sbin/ip route|awk '/default/ { print $3 }'` >>  /usr/local/etc/php/php.ini
## RUN  echo "xdebug.remote_host=docker.for.windows.localhost" >> /usr/local/etc/php/php.ini
## docker.for.windows.localhost didn't work somehow in company, only at home, therefore using 10.0.75.1 docker bridge,
## docker.for.windows.localhost  is confused by VirtualBox hostonly
##RUN  echo "xdebug.remote_host=10.0.75.1" >> /usr/local/etc/php/php.ini
## use docker ip inside VirtualBox, according to needs
#RUN  echo "xdebug.remote_host=172.19.0.1" >> /usr/local/etc/php/php.ini
#RUN  echo 'xdebug.idekey=PHPSTORM' >> /usr/local/etc/php/php.ini
## connectback is after all usable in combination with remote_host, especially for docker CLI calls origins
#RUN  echo 'xdebug.remote_connect_back=1' >> /usr/local/etc/php/php.ini
#RUN  echo 'xdebug.remote_autostart=off' >> /usr/local/etc/php/php.ini
#RUN  echo 'upload_max_filesize = 40M' >> /usr/local/etc/php/php.ini
#RUN  echo 'post_max_size = 40M' >> /usr/local/etc/php/php.ini



RUN echo 'Listen 8080' > /etc/apache2/ports.conf

RUN chmod 0777 /etc/passwd


RUN chmod 0777 /etc/group


RUN chmod -R 0777 /etc/php

RUN chmod -R 0777 /var/log/apache2
RUN chmod -R 0777 /var/log/
RUN chmod -R 0777 /var/lock/apache2
RUN chmod -R 0777 /var/run/apache2
RUN chmod -R 0777 /var/run/
RUN chmod -R 0777 /etc/init.d
RUN chmod -R a+x /var/run/
RUN chmod -R a+x /run

RUN chmod -R 0777 /var/www/html
RUN chmod -R 0777 /var/lib/apache2

RUN chmod -R 0777 /etc/apache2

# openshiftize fpm
RUN sed -i "s/;error_log = log\/php7\/error.log/error_log = \/dev\/stderr/" /etc/php/5.6/fpm/php-fpm.conf
RUN sed -i "s/;error_log = log\/php7\/error.log/error_log = \/dev\/stderr/" /etc/php/7.0/fpm/php-fpm.conf
RUN sed -i "s/;error_log = log\/php7\/error.log/error_log = \/dev\/stderr/" /etc/php/7.1/fpm/php-fpm.conf
RUN sed -i "s/;error_log = log\/php7\/error.log/error_log = \/dev\/stderr/" /etc/php/7.2/fpm/php-fpm.conf


COPY ./php-fpm5.6-www.conf /etc/php/5.6/fpm/pool.d/www.conf
COPY ./php-fpm7.0-www.conf /etc/php/7.0/fpm/pool.d/www.conf
COPY ./php-fpm7.1-www.conf /etc/php/7.1/fpm/pool.d/www.conf
COPY ./php-fpm7.2-www.conf /etc/php/7.2/fpm/pool.d/www.conf


RUN phpenmod -v 7.2 xdebug && phpenmod -v 7.1 xdebug && phpenmod -v 7.0 xdebug && phpenmod -v 5.6 xdebug

RUN phpenmod -v 7.2 memcache && phpenmod -v 7.1 memcache  && phpenmod -v 7.0 memcache  && phpenmod -v 5.6 memcache


RUN  echo "xdebug.remote_port=9000\n\
xdebug.remote_enable=1\n\
xdebug.remote_handler=dbgp\n\
xdebug.idekey=PHPSTORM\n\
xdebug.profiler_enable_trigger = 1\n\
xdebug.remote_connect_back=0\n\
xdebug.remote_autostart=off\n\
upload_max_filesize = 40M\n\
post_max_size = 40M" | tee -a /etc/php/7.2/fpm/conf.d/20-xdebug.ini \
/etc/php/7.1/fpm/conf.d/20-xdebug.ini \
/etc/php/7.0/fpm/conf.d/20-xdebug.ini \
/etc/php/5.6/fpm/conf.d/20-xdebug.ini ;

RUN /sbin/ip route|awk '/default/ { print $3 }'|xargs -I{} echo "xdebug.remote_host={}"| tee -a /etc/php/7.2/fpm/conf.d/20-xdebug.ini \
                                                         /etc/php/7.1/fpm/conf.d/20-xdebug.ini \
                                                         /etc/php/7.0/fpm/conf.d/20-xdebug.ini \
                                                         /etc/php/5.6/fpm/conf.d/20-xdebug.ini && \
                                                                                               cat /etc/php/7.2/fpm/conf.d/20-xdebug.ini

# for bamboo build
#COPY   ./efse       /var/www/html/efse


# && apache2ctl -k restart -D FOREGROUND

#CMD bash -c 'service php5.6-fpm restart & \
#          service php7.2-fpm restart & \
#          apache2ctl -k restart & \
#          (echo echo "127.0.0.1 php72.localhost" >> /etc/hosts || tail -f /dev/null)'


# ENTRYPOINT is executed prior and even inside docker compose unlike CMD
ENTRYPOINT /bin/bash \
        #| /bin/sh   echo "127.0.0.1 php56.localhost" >> /etc/hosts &  echo "127.0.0.1 php72.localhost" >> /etc/hosts  \
        &  service php5.6-fpm restart \
        &  service php7.0-fpm restart \
        &  service php7.1-fpm restart \
        &  service php7.2-fpm restart \
        & apache2ctl -k restart  -D FOREGROUND \
        & tail -f /dev/null


CMD /bin/bash -c 'service php5.6-fpm restart \
        &  service php7.0-fpm restart \
        &  service php7.2-fpm restart \
        & apache2ctl -k restart  -D FOREGROUND \
        & tail -f /dev/null'


#CMD bash -c 'service php5.6-fpm restart & \
#          service php7.2-fpm restart & \
#          apache2ctl -k restart & \
#          (echo echo "127.0.0.1 php72.localhost" >> /etc/hosts || tail -f /dev/null)'


#ENTRYPOINT bash -c 'service php5.6-fpm restart & \
#          service php7.2-fpm restart & \
#          apache2ctl -k restart  -D FOREGROUND & \
#          (echo echo "127.0.0.1 php72.localhost" >> /etc/hosts || tail -f /dev/null)'


#CMD echo 127.0.0.1 php56.localhost > /etc/hosts && php72.localhost > /etc/hosts |  tail -f /dev/null


#RUN apk add --update

