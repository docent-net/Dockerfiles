# Based on the Fedora image
FROM fedora

MAINTAINER "Maciej Lasyk" <maciek@lasyk.info>

# install main packages:
RUN yum -y update

# firstly let's install postgres - following scollier's Dockerfile from https://git.fedorahosted.org/cgit/dockerfiles.git/tree/postgres
RUN yum -y install postgresql-server postgresql postgresql-contrib supervisor
ADD ./postgresql-setup /usr/bin/postgresql-setup
ADD ./postgres_user.sh /postgres_user.sh
ADD ./supervisord.conf /etc/supervisord.conf
ADD ./start_postgres.sh /start_postgres.sh

RUN chmod +x /usr/bin/postgresql-setup
RUN chmod +x /start_postgres.sh
RUN chmod +x /postgres_user.sh

RUN /usr/bin/postgresql-setup initdb

ADD ./postgresql.conf /var/lib/pgsql/data/postgresql.conf

RUN chown -v postgres.postgres /var/lib/pgsql/data/postgresql.conf

RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf

RUN /postgres_user.sh

# now let's install FAS:
RUN yum -y install git-core postgresql-plpython postgresql-server postgresql-python python-TurboMail TurboGears pygpgme python-sqlalchemy python-genshi python-psycopg2 pytz python-babel babel python-GeoIP python-openid python-fedora-turbogears python-migrate python-memcached python-tgcaptcha2 pyOpenSSL gettext python-imaging python-pwquality tulrich-tuffy-fonts
