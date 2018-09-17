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

# add ETS for Security Client 1.0
ADD ets-security-client10-*-ctl.zip /root/
RUN cd /root/ && unzip -q ets-security-client10-*-ctl.zip -d /root/te_base/scripts
ADD ets-security-client10-*-deps.zip /root/
RUN cd /root/ && unzip -q -o ets-security-client10-*-deps.zip -d /usr/local/tomcat/webapps/teamengine/WEB-INF/lib

# Extract sample JKS to root
# Can be used in CTL script as a test run property at path
# /root/ets-security-client10.jks
RUN unzip -j "/usr/local/tomcat/webapps/teamengine/WEB-INF/lib/ets-security-client10-*.jar" "security.jks" -d "/root"
RUN mv /root/security.jks /root/ets-security-client10.jks

# run tomcat
CMD ["catalina.sh", "run"]
