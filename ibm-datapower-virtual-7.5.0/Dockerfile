FROM ubuntu:trusty

# Place only one common deb and one image deb in the local directory
# before running docker build
COPY ibm-datapower-common.deb ibm-datapower-image.deb /tmp/

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies, enable web-mgmt, prepare for first run
RUN echo "Installing dependencies" \
    && apt-get update \
    && apt-get -y install \
          kpartx \
          schroot \
          telnet \
    && echo "Installing DataPower Packages" \
    && dpkg -i /tmp/ibm-datapower-common.deb /tmp/ibm-datapower-image.deb \
    && echo "Enabling WebGUI" \
    && sed -i \
          -e '/^web-mgmt/,/^exit/s/admin-state.*/admin-state "enabled"/g' \
          /opt/ibm/datapower/datapower-external.cfg \
    && echo "Removing intermediate package files" \
    && rm /tmp/ibm-datapower-common.deb /tmp/ibm-datapower-image.deb \
    && echo "Preparing to run" \
    && /opt/ibm/datapower/datapower-docker-build.sh \
    && mkdir -p /datapower/config /datapower/local \
    && echo "DataPowerConfigDir=/datapower/config" >> /opt/ibm/datapower/datapower.conf \
    && echo "DataPowerLocalDir=/datapower/local" >> /opt/ibm/datapower/datapower.conf \
    && echo "DataPowerCpuCount=4" >> /opt/ibm/datapower/datapower.conf

# EXPOSE the port for the WebGUI
EXPOSE 9090

CMD ["/opt/ibm/datapower/datapower-launch"]