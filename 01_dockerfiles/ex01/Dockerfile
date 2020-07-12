FROM  debian:10

ARG   HOME_DIR=/opt/ts3server
ARG   TEAMSPEAK_URL=https://files.teamspeak-services.com/releases/server/3.12.1/teamspeak3-server_linux_amd64-3.12.1.tar.bz2

# to accept license
ENV TS3SERVER_LICENSE=accept

ENV PATH "${PATH}:${HOME_DIR}"

# create non-root user and group to run the server
RUN   adduser --system --home ${HOME_DIR} -group ts3server

WORKDIR  ${HOME_DIR}

RUN   apt-get update && apt-get install curl bzip2 -y && \
      curl ${TEAMSPEAK_URL} | tar -xj --strip-components 1

RUN   chown ts3server:ts3server ${HOME_DIR} -R

#  9987 default voice
# 10011 server query
# 30033 file transport
EXPOSE 9987/udp 10011 30033

# change user
USER  ts3server

ENTRYPOINT ["ts3server_minimal_runscript.sh"]
CMD ["start"]
