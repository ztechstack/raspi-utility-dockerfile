ARG registry=registry
ARG ubuntu_code_name=bionic

FROM ${registry}/ubuntu:${ubuntu_code_name}

ENV ARIANG_VERSION=1.1.4

ARG ARIANG_INSTALL_DEPS="curl unzip"
ARG ARIANG_DL_URL="https://github.com/mayswind/AriaNg/releases/download/${ARIANG_VERSION}/AriaNg-${ARIANG_VERSION}.zip"
ARG ARIANG_DL_PATH="/opt/AriaNg-${ARIANG_VERSION}.zip"

ENV ARIANG_BACKUP_DIR="/opt/.AriaNg-${ARIANG_VERSION}"
ENV ARIANG_ROOT_DIR="/opt/AriaNg-${ARIANG_VERSION}"

RUN apt-get update \
 && apt-get install -y ${ARIANG_INSTALL_DEPS} \
 && curl -fsSL ${ARIANG_DL_URL} -o ${ARIANG_DL_PATH} \
 && cd /opt \
 && unzip -d ${ARIANG_ROOT_DIR} ${ARIANG_DL_PATH} \
 && cp -r ${ARIANG_ROOT_DIR} ${ARIANG_BACKUP_DIR} \
 && rm -Rf ${ARIANG_DL_PATH} \
 && apt-get purge -y --auto-remove ${ARIANG_INSTALL_DEPS} \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

WORKDIR ${ARIANG_ROOT_DIR}

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]