FROM centos:6.9

LABEL  maintainer "Hitoshi Hayakawa <hykw1234@gmail.com>"

# mysql depends on perl, which kerl needs to work
RUN yum -y update && \
    yum -y reinstall glibc-common && \
    yum -y install gcc ctags ncurses-devel openssl-devel mysql && \
    yum clean all && \
    /bin/cp -f /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# needing ja locales, don't call before 'yum reinstall glibc-common'
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"

ENV ERL_VER="20.1"

RUN \
  cd /tmp && \
  curl -O https://raw.githubusercontent.com/spawngrid/kerl/master/kerl && \
  chmod +x kerl && \
  ./kerl list releases && \
  ./kerl build ${ERL_VER} build${ERL_VER} && \
  mkdir -p /usr/local/erl/${ERL_VER} && \
  ./kerl install build${ERL_VER} /usr/local/erl/${ERL_VER} && \
  rm -rf ~/.kerl
