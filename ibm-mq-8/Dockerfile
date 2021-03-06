FROM ubuntu:14.04

RUN export DEBIAN_FRONTEND=noninteractive \
  # The URL to download the MQ installer from in tar.gz format
  && MQ_URL=http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/messaging/mqadv/mqadv_dev80_linux_x86-64.tar.gz \
  # The MQ packages to install
  && MQ_PACKAGES="MQSeriesRuntime-*.rpm MQSeriesServer-*.rpm MQSeriesMsg*.rpm MQSeriesJava*.rpm MQSeriesJRE*.rpm MQSeriesGSKit*.rpm" \
  # Optional: Update the command prompt
  && echo "mq:8.0" > /etc/debian_chroot \
  # Install additional packages required by this install process and the runtime scripts
  && apt-get update -y \
  && apt-get install -y \
    bash \
    bc \
    curl \
    rpm \
    tar \
  # Download and extract the MQ installation files
  && mkdir -p /tmp/mq \
  && cd /tmp/mq \
  && curl -LO $MQ_URL \
  && tar -zxvf ./*.tar.gz \
  # Recommended: Create the mqm user ID with a fixed UID and group, so that the file permissions work between different images
  && groupadd --gid 1000 mqm \
  && useradd --uid 1000 --gid mqm --home-dir /var/mqm mqm \
  && usermod -G mqm root \
  && cd /tmp/mq/MQServer \
  # Accept the MQ license
  && ./mqlicense.sh -text_only -accept \
  # Install MQ using the RPM packages
  && rpm -ivh --force-debian $MQ_PACKAGES \
  # Recommended: Set the default MQ installation (makes the MQ commands available on the PATH)
  && /opt/mqm/bin/setmqinst -p /opt/mqm -i \
  # Clean up all the downloaded files
  && rm -rf /tmp/mq

COPY *.sh /usr/local/bin/
COPY *.mqsc /etc/mqm/

# Support the latest functional cmdlevel by default
ENV MQ_QMGR_CMDLEVEL=802

RUN chmod +x /usr/local/bin/*.sh

# Uses port 1414
EXPOSE 1414

# Puts the MQ data directory in a Docker volume
VOLUME /var/mqm

ENTRYPOINT ["mq.sh"]
