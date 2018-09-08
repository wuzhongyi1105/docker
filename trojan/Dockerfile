FROM alpine
LABEL maintainer="imlonghao"
ARG version=1.7.0
WORKDIR /app
RUN apk add --no-cache --virtual build-dependencies cmake g++ make boost-dev && \
    apk add --no-cache mariadb-dev && \
    wget https://github.com/trojan-gfw/trojan/archive/v${version}.tar.gz && \
    tar zxf v${version}.tar.gz && \
    cd trojan-${version} && \
    sed -i '1iSET(Boost_USE_STATIC_LIBS ON)' CMakeLists.txt && \
    sed -i '1iSET(CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++")' CMakeLists.txt && \
    cmake . && \
    make && \
    mv trojan /app && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk /usr/share/man /app/trojan-${version} /app/v${version}.tar.gz
EXPOSE 1080
ENTRYPOINT [ "/app/trojan" ]
CMD [ "conf/config.json" ]