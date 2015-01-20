FROM jboss/wildfly:8.2.0.Final
MAINTAINER Jorge Morales <jmorales@redhat.com>

ENV APIMAN_VERSION 1.0.1.Final

RUN cd $HOME/wildfly \
 && curl http://downloads.jboss.org/overlord/apiman/$APIMAN_VERSION/apiman-distro-wildfly8-$APIMAN_VERSION-overlay.zip | bsdtar -xvf-

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-c", "standalone-apiman.xml"]

