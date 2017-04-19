FROM ubuntu:14.04

# Install Python dependency packages
RUN apt-get update
RUN apt-get -y install python-setuptools
RUN easy_install pip
RUN apt-get -y install python-dev libmysqlclient-dev zlib1g-dev python2.7-dev libpython2.7-dev libexpat1-dev libc-dev gcc
RUN pip install MySQL-python
RUN pip install tornado
RUN pip install SQLAlchemy
RUN pip install backports.ssl_match_hostname
RUN pip install certifi

# Create the directory for Tornado script
RUN mkdir -p /opt/python/scripts
COPY ./tornado_hello_world_web_app.py /opt/python/scripts/tornado_hello_world_web_app.py

# Define mountable directories.
VOLUME ["/opt/python/scripts"]

# Expose Tornado ports from the container to the host
# 8015: Tornado process listening port
EXPOSE 8015

# Run /usr/bin/python with controle_mirror.py
ENTRYPOINT ["/usr/bin/python", "/opt/python/scripts/tornado_hello_world_web_app.py"]


