FROM clearwater/base
MAINTAINER maintainers@projectclearwater.org

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes clearwater-memcached
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes astaire
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes rogers

COPY memcached.supervisord.conf /etc/supervisor/conf.d/memcached.conf
COPY astaire.supervisord.conf /etc/supervisor/conf.d/astaire.conf
COPY rogers.supervisord.conf /etc/supervisor/conf.d/rogers.conf
COPY clearwater-group.supervisord.conf /etc/supervisor/conf.d/clearwater-group.conf

RUN sed -i 's/^.*ptrace_scope.*$//' /etc/init.d/astaire
RUN sed -i 's/^.*ulimit.*$//' /etc/init.d/astaire
RUN sed -i 's/^.*ptrace_scope.*$//' /etc/init.d/rogers
RUN sed -i 's/^.*ulimit.*$//' /etc/init.d/rogers

RUN sed -i 's#mv /tmp/hosts\.\$\$#cat /tmp/hosts.$$ > #' /usr/share/clearwater/infrastructure/scripts/*host*


EXPOSE 11311
