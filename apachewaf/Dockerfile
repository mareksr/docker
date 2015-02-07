#
# dododoosdiaodiasodiaoidoaidoaidoaidoaidoaidoaidoaidoaidoaidoiaidoasido

FROM centos
MAINTAINER marek <mareksr@hm.pl>

RUN yum update -y
RUN yum install -y wget tar make gcc gcc-c++ perl libxml2-devel expat-devel libcurl-devel git python-setuptools
RUN easy_install supervisor
RUN wget http://ftp.ps.pl/pub/apache//apr/apr-1.5.1.tar.gz
RUN wget http://ftp.ps.pl/pub/apache//apr/apr-util-1.5.4.tar.gz
RUN wget https://www.modsecurity.org/tarball/2.8.0/modsecurity-2.8.0.tar.gz
RUN gzip -cd apr-1.5.1.tar.gz | tar vxf -
RUN gzip -cd apr-util-1.5.4.tar.gz | tar vxf -
RUN gzip -cd modsecurity-2.8.0.tar.gz | tar vxf -
RUN cd apr-1.5.1 && ./configure --prefix=/usr/local/apr-1.5.1 && make && make install
RUN cd apr-util-1.5.4 && ./configure --prefix=/usr/local/apr-util-1.5.4 --with-apr=/usr/local/apr-1.5.1 && make && make install
RUN wget http://apache.mirrors.hoobly.com//httpd/httpd-2.2.29.tar.gz

RUN wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.36.tar.gz
RUN gzip -cd pcre-8.36.tar.gz | tar vxf -
RUN cd pcre-8.36 && ./configure --prefix=/usr/local/pcre-8.36  && make && make install

RUN gzip -cd httpd-2.2.29.tar.gz | tar vxf -
RUN cd httpd-2.2.29 && ./configure  --enable-unique-id --with-pcre=/usr/local/pcre-8.36 --enable-proxy --with-apr=/usr/local/apr-1.5.1 --with-apr-util=/usr/local/apr-util-1.5.4 --prefix=/usr/local/apache2 && make && make install
RUN cd modsecurity-2.8.0 && ./configure  --with-pcre=/usr/local/pcre-8.36 --with-apr=/usr/local/apr-1.5.1 --with-apu=/usr/local/apr-util-1.5.4 && make && make install
RUN git clone https://github.com/gnif/mod_rpaf.git
RUN cd mod_rpaf && sed -i 's/.\/apxs\.sh/\/usr\/local\/apache2\/bin\/apxs/' Makefile && make && make install

RUN rm -rf httpd-2.2.29
RUN rm -rf apr-1.5.1
RUN rm -rf apr-util-1.5.4
RUN rm -rf pcre-8.36
RUN rm -rf mod_rpaf

RUN ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

COPY supervisord.conf /etc/supervisord.conf
CMD /usr/bin/supervisord -c /etc/supervisord.conf




