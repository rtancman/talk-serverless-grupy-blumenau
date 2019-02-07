FROM amazonlinux

RUN yum update -y
RUN yum groupinstall "Development Tools" -y
RUN yum install -y \
    gcc \
    bzip2-devel \
    libffi \
    openssl-devel \
    perl-core \
    zlib-devel \
    libxml2-devel \
    libxslt-devel \
    libffi-devel \
    libcffi-devel \
    wget \
    postgresql96-devel \
    mysql56-devel \
    sqlite

RUN curl -O http://download.redis.io/redis-stable.tar.gz && \
    tar xvf redis-stable.tar.gz && \
    cd redis-stable && \
    make && make install && rm -rf redis-stable.tar.gz

ENV PYTHON_VERSION 3.7.2

RUN cd /usr/src/ && \
    wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz && \
    tar xzf Python-$PYTHON_VERSION.tgz && \
    cd Python-$PYTHON_VERSION && \
    ./configure --enable-optimizations && \
    make altinstall && \
    cd / && rm -rf /usr/src/Python-$PYTHON_VERSION.tgz && python3.7 -V

RUN pip3.7 install --upgrade pip && pip3.7 install awscli setuptools wheel

RUN mkdir /app
WORKDIR /app

CMD /bin/bash