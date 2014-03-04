# This was tested using:
#   ElasticSearch 1.0.1
#
#
# If you want to use another versions please edit this file and replace URLs
# for packages / tarballs

# Based on the Fedora image
FROM fedora

MAINTAINER "Maciej Lasyk" <maciek@lasyk.info>

# install main packages:
RUN yum -y update
RUN yum -y install java gcc gcc-c++ rubygems rubygems-devel ruby ruby-devel nginx rsyslog wget supervisor

# temporary devenv packages:
RUN yum -y install net-tools vim which mlocate netstat

ADD ./supervisord.d/elasticsearch.ini /etc/supervisord.d/elasticsearch.ini

# install elasticsearch:
RUN mkdir /usr/src/rpms -p
WORKDIR /usr/src/rpms
RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.0.1.noarch.rpm
RUN yum localinstall -y elasticsearch-1.0.1.noarch.rpm

# set the env:
#RUN useradd -d /home/twitter twitter
#USER twitter 
#ENV HOME /home/twitter
#WORKDIR /home/twitter

CMD ["supervisord", "-n", "-c /etc/supervisord.conf"]
