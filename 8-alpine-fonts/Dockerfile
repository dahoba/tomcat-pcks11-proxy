FROM tomcat:8-alpine
LABEL MAINTAINER SiritasDho<dahoba@gmail.com>

RUN apk --update --no-cache add \
        alpine-sdk \
        autoconf \
        automake \
        git \
        curl \
        unzip \
        libtool \
        libseccomp-dev \
        cmake \
        p11-kit-dev \
        openssl-dev \
        fontconfig

RUN curl -q -o "/tmp/sarabun-fonts.zip" -LO https://github.com/cadsondemak/Sarabun/archive/master.zip && \
    unzip /tmp/sarabun-fonts.zip -d /tmp/ && \
    mkdir -p /usr/share/fonts/ && \
    cp /tmp/Sarabun-master/fonts/*.ttf /usr/share/fonts/ && \
    fc-cache -f

WORKDIR /tmp/pkcs11-proxy
RUN git clone https://github.com/SUNET/pkcs11-proxy /tmp/pkcs11-proxy && \
    cd /tmp/pkcs11-proxy && \
    cmake . && make && make install

WORKDIR $CATALINA_HOME
RUN rm -rf /tmp/pkcs11-proxy /tmp/sarabun-fonts.zip
RUN apk --update --no-cache add opensc openssl stunnel

EXPOSE 5658
EXPOSE 8080
ENV PKCS11_PROXY_SOCKET="tcp://softhsm:5657"
CMD ["catalina.sh", "run"]
