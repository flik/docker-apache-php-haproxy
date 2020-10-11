FROM centos:centos7

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum-config-manager --enable remi-php73 -y

# INSTALL APACHE AND PHP PACKAGES (Apache 2.4 & PHP 7)
RUN     yum -y update \
        && yum --setopt=tsflags=nodocs -y install \
        php \
        php-mcrypt \
        php-bcmath \
        php-intl \
        php-cli \
        php-gd \
        php-curl \
        php-mysql \
        php-devel \
        php-mysql \
        php-pdo \
        php-mbstring \
        php-zip \
        php-soap \
        php-gd \
        php-xml \
        php-mysqlnd \
        php-pecl-zip \
        freetype \
        fontconfig \
        php-json \
        unzip \
        httpd \
        httpd-tools \
        apr \
        apr-util \
        && rm -rf /var/cache/yum/* \
        && yum clean all

# RUN mkdir -p /var/www/html/public
# ENV APP_HOME /var/www/html

# change ownership of our applications
# RUN chown -R www-data:www-data $APP_HOME
RUN curl -s https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
COPY index.php /var/www/html/index.php

COPY httpd.conf /etc/httpd/conf/httpd.conf
#RUN systemctl restart httpd
RUN yum -y install librdkafka-devel

RUN yum install -y java-1.8.0-openjdk
#RUN yum install -y https://archive.cloudera.com/cdh5/one-click-install/redhat/7/x86_64/cloudera-cdh-5-0.x86_64.rpm

#RUN yum install -y zookeeper

# zookeper example
#RUN cd /tmp
#RUN curl -s https://pecl.php.net/get/zookeeper-0.2.2.tgz | tar zxvf -
#RUN cd zookeeper-0.2.2 && ls \
#&& phpize ./configure --with-php-config=/usr/local/php/bin/php-config  --with-libzookeeper-dir=/usr/local/zookeeper \
#&&  make && make install

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
