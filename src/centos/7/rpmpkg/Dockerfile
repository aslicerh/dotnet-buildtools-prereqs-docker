#FROM mcr.microsoft.com/dotnet-buildtools/prereqs:centos-7-local
FROM centos:7

ENV RUBY_SCL="rh-ruby26"

RUN yum install -y centos-release-scl-rh centos-release-scl

# Install the rpm packaging toolchain required to build rpms
RUN yum clean all \
    #&& yum --enablerepo=centos-sclo-rh -y install ${RUBY_SCL} \
    #&& yum --enablerepo=centos-sclo-rh -y install ${RUBY_SCL}-ruby-devel \
    #&& yum --enablerepo=centos-sclo-rh -y install ${RUBY_SCL}-rubygems \
    && yum install -y \
        gcc \
        rpm-build \
        make \
        centos-release-scl \
        ${RUBY_SCL} \
        ${RUBY_SCL}-ruby-devel \
        ${RUBY_SCL}-rubygems \
        scl-utils \
    && yum clean all \
    && scl enable ${RUBY_SCL} 'gem install --no-document fpm git:1.7.0 ffi:1.12.2'

ENV CONTAINER_SCRIPTS_PATH=/opt/app-root \
    ENABLED_COLLECTIONS="${RUBY_SCL}"

COPY ./scl_enable ${CONTAINER_SCRIPTS_PATH}/etc/scl_enable

# When bash is started non-interactively, to run a shell script, for example it
# looks for this variable and source the content of this file. This will enable
# the SCL for all scripts without need to do 'scl enable'.
ENV BASH_ENV=${CONTAINER_SCRIPTS_PATH}/etc/scl_enable \
    ENV=${CONTAINER_SCRIPTS_PATH}/etc/scl_enable \
    PROMPT_COMMAND=". ${CONTAINER_SCRIPTS_PATH}/etc/scl_enable"
