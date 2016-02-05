FROM java:8
MAINTAINER Eliot Kimber "ekimber@contrext.com"
# Make directories for later use
ENV OT_VERSION 1.8.5
LABEL ot-version ${OT_VERSION}
RUN chmod -R a+rwx /opt

ENV HOME /home/dita-ot
ENV DITA_HOME $HOME/DITA-OT
ENV ANT_HOME $DITA_HOME/tools/ant
ENV PATH $ANT_HOME/bin:$DITA_HOME:$PATH
WORKDIR $HOME
RUN wget -O dita-ot-${OT_VERSION}.zip -c http://sourceforge.net/projects/dita-ot/files/DITA-OT%20Stable%20Release/DITA%20Open%20Toolkit%201.8/DITA-OT1.8.5_full_easy_install_bin.zip/download && \
  unzip dita-ot-${OT_VERSION}.zip && \
  rm dita-ot-${OT_VERSION}.zip
# Use a consistent name for the OT so we don't have to worry about it
RUN mv $HOME/DITA-OT${OT_VERSION} $DITA_HOME
# Set execution permissions on ant/bin directory
RUN chmod a+rwx $ANT_HOME/bin/* 
# Put the bin directory in the path:
ENV PATH $ANT_HOME/bin:$PATH
WORKDIR $DITA_HOME
# Prepare the /opt/dita-ot/DITA-OT directory
# so it can be used as a volume:
RUN mkdir -p /opt/dita-ot
RUN ln -s $DITA_HOME /opt/dita-ot/DITA-OT
#
# Set up the Java classpath as defined in startcmd.sh:
#
ENV CLASSPATH $DITA_HOME/lib/dost.jar:\
$DITA_HOME/lib:\
$DITA_HOME/lib/commons-codec-1.4.jar:\
$DITA_HOME/lib/resolver.jar:\
$DITA_HOME/lib/icu4j.jar:\
$DITA_HOME/lib/xercesImpl.jar:\
$DITA_HOME/lib/xml-apis.jar:\
$DITA_HOME/lib/saxon/saxon9.jar:\
$DITA_HOME/lib/saxon/saxon9-dom.jar
#
# Declare volumes intended to be mount points for
# host directories:
VOLUME /opt/dita-ot/data
VOLUME /opt/dita-ot/out
#
# End of Dockerfile
#