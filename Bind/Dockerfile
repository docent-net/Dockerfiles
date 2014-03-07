# Based on the Fedora image
FROM fedora

MAINTAINER "Maciej Lasyk" <maciek@lasyk.info>

# install main packages:
RUN yum -y update
RUN yum -y install bind-utils bind cronie logrotate

# gen rndc key:
RUN rndc-confgen -a -c /etc/rndc.key

ADD ./cfg_files/rsyslogd.d/20-bind.conf /etc/rsyslogd.d/20-bind.conf
ADD ./cfg_files/logrotate.d/named /etc/logrotate.d/named
ADD ./cfg_files/init.d/named /etc/init.d/named
RUN chmod +x /etc/init.d/named
RUN mkdir /var/dockerlock/subsys -p

# set the env:
CMD ["/usr/sbin/crond"]
CMD ["/etc/init.d/named","start"]
