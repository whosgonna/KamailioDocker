ARG DEB_VER=13
ARG KAM_VER=61
ARG SIPEXER_VER=1.2.0

FROM debian:${DEB_VER}-slim
ARG DEB_VER
ARG KAM_VER
ARG SIPEXER_VER
ARG TARGETARCH

RUN    apt update \
    && apt install -y wget gpg vim sngrep \
    && KAM_GPG_KEY="https://deb.kamailio.org/kamailiodebkey.gpg" \
    && KEYRING="/usr/share/keyrings/kamailio.gpg" \
    && KAM_REPO="http://deb.kamailio.org/kamailio${KAM_VER}" \
    && APT_LIST="/etc/apt/sources.list.d/kamailio.list" \
    &&  . /etc/os-release \
    && wget -O- $KAM_GPG_KEY | gpg --dearmor > $KEYRING \
    && APT_STR="[signed-by=${KEYRING}] ${KAM_REPO} ${VERSION_CODENAME} main" \
    && echo "deb     ${APT_STR}" > $APT_LIST \
    && echo "deb-src ${APT_STR}" >> $APT_LIST  \
    && apt update \
    && apt install -y \
        kamailio kamailio-authblockchain-modules kamailio-autheph-modules \
        kamailio-cnxcc-modules kamailio-cpl-modules kamailio-erlang-modules \
        kamailio-extra-modules kamailio-geoip2-modules kamailio-ims-modules \
        kamailio-json-modules kamailio-kafka-modules kamailio-kazoo-modules \
        kamailio-ldap-modules kamailio-lua-modules kamailio-lwsc-modules \
        kamailio-memcached-modules kamailio-microhttpd-modules \
        kamailio-mongodb-modules kamailio-mqtt-modules kamailio-mysql-modules \
        kamailio-nats-modules kamailio-nth kamailio-outbound-modules \
        kamailio-outbound-modules kamailio-perl-modules kamailio-phonenum-modules \
        kamailio-postgres-modules kamailio-presence-modules kamailio-python3-modules \
        kamailio-rabbitmq-modules kamailio-radius-modules kamailio-ruby-modules \
        kamailio-sctp-modules kamailio-secsipid-modules kamailio-snmpstats-modules \
        kamailio-sqlite-modules kamailio-tls-modules kamailio-tls-wolfssl-modules \
        kamailio-unixodbc-modules kamailio-utils-modules kamailio-websocket-modules \
        kamailio-xml-modules kamailio-xmpp-modules kamcli \
\
    && SIPEXER_URL="https://github.com/miconda/sipexer/releases/download" \
    && SIPEXER_VER="v${SIPEXER_VER}" \
    && SIPEXER_FILE="sipexer-${SIPEXER_VER}-linux-${TARGETARCH}.tar.gz" \
    && wget ${SIPEXER_URL}/${SIPEXER_VER}/${SIPEXER_FILE} \
    && tar -xf ${SIPEXER_FILE} \
    && mv sipexer /usr/bin/sipexer \
    && rm -f ${SIPEXER_FILE} \
\
    && apt clean \
    && rm -rf /var/lib/apt/lists/* 


## For the benefit of sngrep
ENV TERM=screen

ENTRYPOINT ["/usr/sbin/kamailio", "-DDEd"]

