# Download base redis image
FROM redis:5.0-alpine

MAINTAINER Taehyoung Yim <taehyoung.yim@bespinglobal.com>

## Copy Redis File
RUN rm -rf /usr/local/bin/docker-entrypoint.sh
ADD redis.conf /usr/local/bin/redis.conf
ADD docker-entrypoint.sh /usr/local/bin

## change access authority
RUN chmod 755 /usr/local/bin/redis.conf
RUN chmod 755 /usr/local/bin/docker-entrypoint.sh

RUN chown redis:redis /usr/local/bin/redis.conf
RUN chown redis:redis /usr/local/bin/docker-entrypoint.sh

# Redis Container에 대한 Port를 지정합니다. (내부포트이며 외부노출은 안됨)
# CLIENTPORT에 대한 값은 docker-compose.yml에 정의되어 있습니다.
EXPOSE $CLIENTPORT

# Container가 생성, 시작하는 시점에 실행됩니다.
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

# Container 빌드가 완료되고 Redis Server를 실행시킵니다.
CMD [ "redis-server","/usr/local/bin/redis.conf" ]