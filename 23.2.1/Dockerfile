FROM centos:7.9.2009

LABEL  maintainer "Hitoshi Hayakawa <hykw1234@gmail.com>"

RUN yum -y update && \
    yum -y reinstall glibc-common && \
    yum -y install gcc gcc-c++ glibc-devel ctags ncurses-devel openssl-devel mysql git && \
    yum -y install autoconf automake make && \
    yum clean all && \
    /bin/cp -f /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# ja locales require, never call before 'yum reinstall glibc-common'
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"

ENV ERL_VER="23.2.1"

RUN \
  cd /tmp && \
  curl -O https://raw.githubusercontent.com/spawngrid/kerl/master/kerl && \
  chmod +x kerl && \
  ./kerl update releases && \
  ./kerl build ${ERL_VER} build${ERL_VER} && \
  mkdir -p /usr/local/erl/${ERL_VER} && \
  ./kerl install build${ERL_VER} /usr/local/erl/${ERL_VER} && \
  rm -rf ~/.kerl
