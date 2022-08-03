FROM centos:7
MAINTAINER Hess Lee <hess.lee@altibase.com>
RUN mkdir /home/altibase
ENV HOME=/home/altibase
SHELL ["/bin/bash"]
WORKDIR /home/altibase
COPY altibase_home.tgz /home/altibase
RUN tar 
RUN rm /home/altibase/altibase_home.tgz
RUN cp /home/altibase/altibase_home/conf/altibase.properties.shard /home/altibase/altibase_home/conf/altibase.properties
RUN rm -rf /home/altibase/altibase_home/dbs
RUN rm -rf /home/altibase/altibase_home/logs
RUN rm -rf /home/altibase/altibase_home/xlogs
RUN rm -rf /home/altibase/altibase_home/arch_logs
RUN rm -rf /home/altibase/altibase_home/trc
RUN rm -rf /home/altibase/altibase_home/ZookeeperServer.tar.gz
RUN rm -rf /home/altibase/altibase_home/ZookeeperServer/apache-zookeeper-3.5.6-bin.tar.gz
