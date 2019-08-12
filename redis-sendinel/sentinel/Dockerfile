# Download base redis-sentinel image
FROM lgatica/redis-sentinel:4.0.2
MAINTAINER Taehyoung Yim <taehyoung.yim@bespinglobal.com>

# Copy redis files for configuration
## Remove previous conf file to change a new conf file
RUN rm -rf /usr/local/bin/sentinel-entrypoint.sh
ADD sentinel.conf /usr/local/bin/sentinel.conf
ADD sentinel-entrypoint.sh /usr/local/bin/sentinel-entrypoint.sh

# Modify access permission and ownership of files
RUN chmod 755 /usr/local/bin/sentinel.conf
RUN chmod 755 /usr/local/bin/sentinel-entrypoint.sh
RUN chown redis:redis /usr/local/bin/sentinel.conf
RUN chown redis:redis /usr/local/bin/sentinel-entrypoint.sh

# Redis Container에 대한 Port를 지정합니다. (내부포트이며 외부노출은 안됨)
# CLIENTPORT에 대한 값은 docker-compose.yml에 정의되어 있습니다.
EXPOSE $CLIENTPORT

# Container가 생성, 시작하는 시점에 실행됩니다.
ENTRYPOINT ["/usr/local/bin/sentinel-entrypoint.sh"]

# Container 빌드가 완료되고 Redis Sentinel를 실행시킵니다.
CMD [ "redis-server","/usr/local/bin/sentinel.conf", "--sentinel" ]
