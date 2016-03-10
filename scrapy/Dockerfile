FROM centos:6.7
MAINTAINER leilei01 "benjaminlei@126.com"

ENV LANG en_US.UTF-8 ENV LC_ALL en_US.UTF-8

RUN yum install -y wget xz tar
RUN yum install -y zlib-devel bzip2-devel zlib-devel bzip2-devel openssl-devel zlib-devel bzip2-devel openssl-devel ncurses-devel zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel python-dev curl libxml2-dev libxslt-dev libffi-dev gcc musl-dev libgcc openssl-dev

RUN mkdir -p /home/source 
WORKDIR /home/source RUN wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tar.xz
WORKDIR /home/source RUN tar xf Python-2.7.11.tar.xz
WORKDIR /home/source/Python-2.7.11 RUN ./configure RUN make RUN make install
RUN wget https://bootstrap.pypa.io/ez_setup.py -O - | python 
RUN easy_install pip
RUN pip install scrapy
CMD ["scrapy"]
