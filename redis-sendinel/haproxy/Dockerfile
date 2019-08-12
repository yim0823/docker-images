# Download base haproxy image
FROM haproxy:1.8.4
MAINTAINER Taehyoung Yim <taehyoung.yim@bespinglobal.com>

## Copy Redis File
## Remove previous conf file to change a new conf file
RUN rm -rf /usr/local/bin/haproxy-entrypoint.sh
ADD haproxy.cfg /usr/local/bin/haproxy.cfg
ADD haproxy-entrypoint.sh /usr/local/bin/haproxy-entrypoint.sh

## change access authority
RUN chmod 755 /usr/local/bin/haproxy.cfg
RUN chmod 755 /usr/local/bin/haproxy-entrypoint.sh

#RUN chown redis:redis /usr/local/bin/haproxy.cfg
#RUN chown redis:redis /usr/local/bin/haproxy-entrypoint.sh

# Redis Container에 대한 Port를 지정합니다.
# MASTER_PORT CLIENT_PORT에 대한 값은 docker-compose.yml에 정의되어 있습니다.
EXPOSE $MASTER_PORT $CLIENT_PORT

# Container가 생성, 시작하는 시점에 실행됩니다.
ENTRYPOINT ["/usr/local/bin/haproxy-entrypoint.sh"]

# Container 빌드가 완료되고 haproxy 를 실행시킵니다.
CMD ["haproxy", "-f", "/usr/local/bin/haproxy.cfg"]