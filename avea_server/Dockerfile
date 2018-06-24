ARG BUILD_FROM
FROM $BUILD_FROM

ENV LANG C.UTF-8

# Install requirements for add-on
RUN apk add --no-cache git nodejs nodejs-npm python make g++ linux-headers bluez bluez-deprecated

# Install avea server
RUN cd /root && export GIT_SSL_NO_VERIFY=1 && \
    git config --global http.sslVerify false && \
    git clone https://github.com/Marmelatze/avea_server.git

WORKDIR /root/avea_server
RUN cd /root/avea_server && npm install

# Install avea_bulb server branch
RUN rm -R /root/avea_server/node_modules/avea_bulb
RUN cd /root/avea_server/node_modules && \
    git clone https://github.com/Marmelatze/avea_bulb.git --branch avea_server

WORKDIR /root/avea_server

# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]