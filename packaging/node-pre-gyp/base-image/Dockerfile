FROM alanfranz/fwd-centos-6:latest

ARG PACKAGECLOUD_URL

ENV NPM_CONFIG_UNSAFE_PERM true

# Install EPEL & devtoolset
# On CentOS6, there is a bug with OverlayFS and Docker. It is needed to touch
# /var/lib/rpm/* in order to work around this issue.
# Link: https://github.com/docker/docker/issues/10180

RUN touch /var/lib/rpm/* \
    && yum -y install \
        epel-release \
        centos-release-scl-rh \
    && yum-config-manager --enable rhel-server-rhscl-6-rpms \
    && curl -s $PACKAGECLOUD_URL/script.rpm.sh | bash \
    && yum -y install \
        python27 \
        which \
        chrpath \
        openssl-devel \
        devtoolset-3-gcc \
        devtoolset-3-gcc-c++ \
        devtoolset-3-binutils \
        libconfig-devel \
        jq \
    && yum remove -y g++ gcc \
    && yum clean all

ENV NVM_DIR /root/.nvm
RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash
RUN . $NVM_DIR/nvm.sh && \
    nvm install 4.4.7 && \
    nvm install 5.12.0 && \
    nvm install 6.5.0 && \
    nvm install 7.0.0
