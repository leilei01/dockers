FROM centos:6.7

RUN yum install -y wget xz tar
RUN yum install -y zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel libssl-dev libffi-devel libxml2 libxml2-devel libxslt libxslt-devel libxml2-dev libxslt1-dev zlib1g-dev libffi-dev

RUN wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tar.xz
RUN tar xf Python-2.7.11.tar.xz&& cd Python-2.7.11 && ./configure && make && make install
RUN wget https://bootstrap.pypa.io/ez_setup.py -O - | python && easy_install pip
RUN pip install scrapy
CMD ["scrapy"]

