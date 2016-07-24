FROM centos:6.7
MAINTAINER leilei01 "benjaminlei@126.com"
         
ENV LANG en_US.UTF-8 ENV LC_ALL en_US.UTF-8
         
RUN yum install -y wget xz tar
RUN yum install -y zlib-devel bzip2-devel zlib-devel bzip2-devel openssl-devel zlib-devel bzip2-devel ncurses-devel ncurses-devel sqlite-devel python-dev curl libffi-devel gcc libgcc libxml2 libxml2-devel libxslt libxslt-devel mysql-devel                                             
         
RUN mkdir -p /home/source
#install MySQL-python 
WORKDIR /home/source/
RUN yum install -y gcc gcc-c++ cmake ncurses-devel bison
RUN useradd -s /sbin/nologin mysql
RUN wget http://dev.mysql.com/get/Downloads/MySQL-5.5/mysql-5.5.50.tar.gz \
         && tar xvf mysql-5.5.50.tar.gz \
         && cd mysql-5.5.50 \
         && cmake -DMYSQL_UNIX_ADDR=/tmp/mysql.sock -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DEXTRA_CHARSETS=all -DWITH_MYISAM_STORAGE_ENGINE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_MEMORY_STORAGE_ENGINE=1 -DWITH_READLINE=1 -DENABLED_LOCAL_INFILE=1 -DMYSQL_DATADIR=/data/mysql/data  -DMYSQL_USER=mysql -DMYSQL_TCP_PORT=3306 \
         && make && make install
#RUN cp /etc/my.cnf /etc/my.cnf.bak \
#         && cp -f support-files/my-innodb-heavy-4G.cnf /etc/my.cnf 

#RUN wget -c http://dev.mysql.com/get/Downloads/MySQL-5.5/MySQL-server-5.5.30-1.el6.x86_64.rpm
#RUN rpm -ivh MySQL-server-5.5.30-1.el6.x86_64.rpm
#RUN wget -c http://dev.mysql.com/get/Downloads/MySQL-5.5/MySQL-client-5.5.30-1.el6.x86_64.rpm
#RUN rpm -ivh MySQL-client-5.5.30-1.el6.x86_64.rpm
#RUN wget -c http://dev.mysql.com/get/Downloads/MySQL-5.5/MySQL-devel-5.5.30-1.el6.x86_64.rpm
#RUN rpm -ivh MySQL-devel-5.5.30-1.el6.x86_64.rpm

RUN wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tar.xz
RUN tar xf Python-2.7.11.tar.xz
WORKDIR /home/source/Python-2.7.11
RUN /bin/bash ./configure
RUN make&& make install
RUN python -V
RUN wget https://bootstrap.pypa.io/ez_setup.py -O - | python
RUN easy_install pip
#install thrift-0.9.1
#RUN wget https://archive.apache.org/dist/thrift/0.9.1/thrift-0.9.1.tar.gz
#RUN tar zxf thrift-0.9.1.tar.gz
#WORKDIR /home/source/thrift-0.9.1/lib/py
#RUN pwd
#RUN python setup.py install
RUN pip install thrift
#install APScheduler 
RUN pip install APScheduler
#RUN wget -c https://pypi.python.org/packages/c8/40/16a2df29261992cee18f6cba9731d9101302cc76d24794a332f6e567fe2f/APScheduler-3.2.0.tar.gz
#RUN tar zxf APScheduler-3.2.0.tar.gz
#WORKDIR /home/source/APScheduler-3.2.0
#RUN python setup.py install
#install DBUtils 
RUN pip install DBUtils 
#install requests 
RUN pip install requests
#clean package
WORKDIR /home
RUN rm -rf source
#useradd work
RUN useradd work
#USER work
CMD ["/bin/bash"]
