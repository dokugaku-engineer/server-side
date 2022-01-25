FROM mysql/mysql-server:8.0.28

RUN microdnf install yum \
  && yum install -y glibc-langpack-ja glibc-locale-source

ENV LANG ja\_JP.UTF-8
