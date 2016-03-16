FROM mhart/alpine-node

ENV KIBANA_VERSION 4.3.1

RUN apk add --update curl && \
  ( curl -Lskj https://download.elastic.co/kibana/kibana/kibana-${KIBANA_VERSION}-linux-x64.tar.gz | \
  gunzip -c - | tar xf - ) && \
  mv /kibana-$KIBANA_VERSION-linux-x64 /kibana && \
  rm -rf /kibana/node && \
  rm /kibana/bin/*.bat

ENV PATH /kibana/bin:$PATH

RUN npm i hapi-auth-cookie
RUN kibana plugin --install elastic/sense
RUN kibana plugin --install kibana-auth-plugin -u https://github.com/hmalphettes/kibana-auth-plugin/archive/master.tar.gz
RUN apk del curl
RUN rm -rfv /var/cache/apk/* /tmp/* /var/tmp/* /root/.npm

ENV LOCAL_AUTH_LOGINS=admin:password
EXPOSE 5601

CMD ["/kibana/bin/kibana"]
