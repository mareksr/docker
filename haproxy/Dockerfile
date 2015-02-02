#


FROM centos
MAINTAINER marek <mareksr@hm.pl>

RUN yum update -y
RUN yum install -y wget tar python-setuptools pcre-devel pcre-static openssl-devel gcc make
RUN easy_install supervisor
RUN wget http://www.haproxy.org/download/1.5/src/haproxy-1.5.11.tar.gz
RUN gzip -cd haproxy-1.5.11.tar.gz | tar vxf -
RUN cd haproxy-1.5.11 &&  make TARGET=linux2628 USE_STATIC_PCRE=1 USE_OPENSSL=1 && make install
COPY supervisord.conf /etc/supervisord.conf

RUN rm -rf haproxy-1.5.11

RUN ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

CMD /usr/bin/supervisord -c /etc/supervisord.conf

#CMD haproxy -f /etc/haproxy/haproxy.cfg





