# Use an official centos runtime as a parent image

FROM centos:7

LABEL maintainer="peace0phmind@gmail.com"

ARG UNIMRCP_VERSION=1.6.0

RUN yum group install -y "Development Tools" \
    && curl -o unimrcp-deps-${UNIMRCP_VERSION}.tar.gz -sSLO http://www.unimrcp.org/project/component-view/unimrcp-deps-1-6-0-tar-gz/download \
    # build unimrcp deps
    && tar -zxf unimrcp-deps-${UNIMRCP_VERSION}.tar.gz \
    && (cd unimrcp-deps-${UNIMRCP_VERSION} \
    && cat build-dep-libs.sh | sed 's/sudo make install/make install/' > build.sh && chmod +x build.sh \
    && ./build.sh -s) \
    && rm -rf unimrcp-deps-${UNIMRCP_VERSION} && rm -f unimrcp-deps-${UNIMRCP_VERSION}.tar.gz \
    # git clone unimrcp
    && git clone --single-branch --branch fox https://github.com/peace0phmind/unimrcp.git

ARG BUILD_VERSION=unknown
RUN (cd unimrcp && echo building at ${BUILD_VERSION} && git pull && ./bootstrap && ./configure && make && make install)
