FROM tomcat:7.0-jre8

MAINTAINER Dirk Stenger <stenger@lat-lon.de>
MAINTAINER Torsten Friebe <friebe@lat-lon.de>

# add TEAM engine webapp
ADD teamengine-web-*.war /root/
RUN cd /root/ && unzip -q teamengine-web-*.war -d /usr/local/tomcat/webapps/teamengine

# add common libs
ADD teamengine-web-*-common-libs.zip /root/
RUN cd /root/ && unzip -q teamengine-web-*-common-libs.zip -d /usr/local/tomcat/lib

# add TEAM engine console
ADD teamengine-console-*-base.zip /root/
RUN cd /root/ && unzip -q teamengine-console-*-base.zip -d /root/te_base

# set TE_BASE
ENV JAVA_OPTS="-Xms1024m -Xmx2048m -DTE_BASE=/root/te_base"

# add ETS for GML 3.2
ADD ets-gml32-*-ctl.zip /root/
RUN cd /root/ && unzip -q ets-gml32-*-ctl.zip -d /root/te_base/scripts
ADD ets-gml32-*-deps.zip /root/
RUN cd /root/ && unzip -q -o ets-gml32-*-deps.zip -d /usr/local/tomcat/webapps/teamengine/WEB-INF/lib

# run tomcat
CMD ["catalina.sh", "run"]