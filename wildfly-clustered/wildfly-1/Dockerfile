FROM jboss/wildfly:latest
USER root
RUN /opt/jboss/wildfly/bin/add-user.sh <username> <password> --silent
ADD standalone-ha.xml /opt/jboss/wildfly/standalone/configuration/
ENV JAVA_OPTS $JAVA_OPTS -Djava.net.preferIPv4Stack=true -Djboss.node.name=pethelp-wildfly1-01 -Djboss.modules.system.pkgs=$JBOSS_MODULES_SYSTEM_PKGS -Djava.awt.headless=true -Djboss.bind.address=192.168.192.6 -Djboss.bind.address.unsecure=192.168.192.6 -Djboss.bind.address.management=192.168.192.6 -server -Xms1024m -Xmx1024m -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:ParallelGCThreads=8 -XX:+CMSParallelRemarkEnabled -XX:NewSize=64m -XX:MaxNewSize=256m -XX:+DisableExplicitGC
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-c", "standalone-ha.xml"]
