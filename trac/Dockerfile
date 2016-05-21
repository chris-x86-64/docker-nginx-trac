FROM centos:latest
MAINTAINER Christopher Smith <chris@x86-64.jp>

# Change this if you're in another timezone
ENV TZ=Asia/Tokyo

RUN yum update -y

RUN yum install -y python-virtualenv gcc \
&& yum clean all
RUN mkdir -p /opt/trac
RUN /usr/bin/virtualenv /opt/python
RUN /opt/python/bin/pip install trac uwsgi

RUN useradd -ms /bin/bash trac
RUN chown -R trac:trac /opt/trac
USER trac
WORKDIR /opt/trac

COPY uwsgi.ini /opt/trac/uwsgi.ini
RUN /opt/python/bin/trac-admin /opt/trac/trac initenv "Your Trac Project Name" "sqlite:db/trac.db"
VOLUME /opt/trac

EXPOSE 7777

CMD /opt/python/bin/uwsgi --enable-threads --uid trac --gid trac --master --processes 8 --die-on-term --ini /opt/trac/uwsgi.ini
