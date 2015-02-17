#
# dododoosdiaodiasodiaoidoaidoaidoaidoaidoaidoaidoaidoaidoaidoiaidoasido

FROM centos
MAINTAINER marek <mareksr@hm.pl>

RUN yum update -y
RUN yum install -y wget tar make gcc gcc-c++ perl libxml2-devel expat-devel libcurl-devel git python-setuptools
RUN easy_install supervisor
RUN wget  http://downloads.sourceforge.net/project/bacula/bacula/7.0.5/bacula-7.0.5.tar.gz 
RUN gzip -cd bacula-7.0.5.tar.gz | tar vxf -
RUN cd bacula-7.0.5 && ./configure --enable-client-only --prefix=/usr/local/bacula-7.0.5 && make && make install
RUN ln -s /usr/local/bacula-7.0.5 /usr/local/bacula 
RUN mkdir -p /usr/local/bacula/var/bacula/working
RUN rm -rf bacula-7.0.5

RUN ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

COPY supervisord.conf /etc/supervisord.conf
CMD /usr/bin/supervisord -c /etc/supervisord.conf




