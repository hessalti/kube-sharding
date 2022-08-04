FROM centos:7

MAINTAINER Hess Lee <hess.lee@altibase.com>

RUN mkdir /home/altibase
ENV HOME=/home/altibase
WORKDIR /home/altibase
USER root

COPY altibase_home.tgz.s* ./
RUN cat altibase_home.tgz.s* > altibase_home.tgz
RUN tar --no-same-owner -xvzf altibase_home.tgz

RUN cp altibase_home/conf/altibase.properties.shard altibase_home/conf/altibase.properties

# remove directory for volume mount
RUN rm -rf altibase_home/dbs
RUN rm -rf altibase_home/logs
RUN rm -rf altibase_home/xlogs
RUN rm -rf altibase_home/arch_logs
RUN rm -rf altibase_home/trc

# remove unnecessary files
RUN rm altibase_home.tgz*
RUN rm -rf altibase_home/ZookeeperServer.tar.gz
RUN rm -rf altibase_home/ZookeeperServer/apache-zookeeper-3.5.6-bin.tar.gz
