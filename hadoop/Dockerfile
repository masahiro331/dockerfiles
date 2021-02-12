FROM centos:8
RUN dnf install -y vim git
RUN dnf group install -y --with-optional 'Development Tools'
RUN dnf install -y java-1.8.0-openjdk-devel maven
RUN dnf install -y python2

RUN git clone https://github.com/protocolbuffers/protobuf && \
  cd protobuf && \
  git checkout v3.7.1 && \
  autoreconf -i && \
  ./configure --prefix=/usr/local && \
  make install
RUN dnf install -y libtirpc-devel zlib-devel lz4-devel bzip2-devel openssl-devel cyrus-sasl-devel libpmem-devel
RUN dnf install -y gcc-toolset-9-gcc gcc-toolset-9-gcc-c++
RUN curl -L https://cmake.org/files/v3.19/cmake-3.19.0.tar.gz > cmake-3.19.0.tar.gz &&\
  tar -zxvf cmake-3.19.0.tar.gz &&\
  cd cmake-3.19.0 &&\
  ./bootstrap &&\
  make -j2 &&\
  make install
RUN curl -L -o boost_1_72_0.tar.bz2 https://sourceforge.net/projects/boost/files/boost/1.72.0/boost_1_72_0.tar.bz2/download &&\
  tar xjf boost_1_72_0.tar.bz2 &&\
  cd boost_1_72_0 &&\
  ./bootstrap.sh --prefix=/usr/local &&\
  ./b2 &&\
  ./b2 install
RUN dnf --enablerepo=powertools install -y snappy-devel
RUN dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm &&\
  dnf --enablerepo=epel install -y libzstd-devel

RUN dnf --enablerepo=powertools install -y nasm &&\
  cd isa-l/ &&\
  ./autogen.sh &&\
  ./configure &&\
  make install

RUN git clone https://github.com/apache/hadoop &&\
  cd hadoop/ &&\
  mvn package -Pdist,native -DskipTests -Dmaven.javadoc.skip
