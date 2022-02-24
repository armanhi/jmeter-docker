FROM ubuntu:20.04
#LABEL Description="This image is used to start the Apache JMeter Master Executable" Vendor="Collabnix" Version="1.0"

ARG JMETER_VERSION="5.4.3"
ARG RANDOM_CSV_VERSION="0.8"
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV	JMETER_BIN	${JMETER_HOME}/bin
ENV JMETER_FILE_PATH apache-jmeter-${JMETER_VERSION}
ENV	JMETER_DOWNLOAD_URL  https://archive.apache.org/dist/jmeter/binaries/${JMETER_FILE_PATH}.tgz
#ENV JMETER_PLUGINS_FOLDER ${JMETER_HOME}/lib/ext/
ENV JMETER_PLUGINS_FOLDER /jmeter/lib/ext/
ENV JMETER_PLUGINS_DOWNLOAD_URL http://repo1.maven.org/maven2/kg/apc
ENV RANDOM_CSV_FILE bzm-random-csv-${RANDOM_CSV_VERSION}.zip

# Installig Pre-requisite Packages like wget & JRE
RUN apt-get clean && \
  apt-get update && \
  apt-get -qy install \
  wget \
  default-jre-headless \
  telnet \
  iputils-ping \
  unzip
# Installing jmeter
RUN mkdir /jmeter \
  && cd /jmeter/ \
  && wget ${JMETER_DOWNLOAD_URL} \
  && tar -xzf ${JMETER_FILE_PATH}.tgz \
  && rm ${JMETER_FILE_PATH}.tgz \
  && wget https://jmeter-plugins.org/files/packages/${RANDOM_CSV_FILE} \
  && unzip ${RANDOM_CSV_FILE} \
  && cp lib/ext/jmeter-plugins-random-csv-data-set-${RANDOM_CSV_VERSION}.jar /lib/ext \
  && cp lib/ext/jmeter-plugins-manager-1.6.jar /lib/ext \
  && rm ${RANDOM_CSV_FILE}
#&& cd ..
#&& mkdir /jmeter-plugins \
#&& cd /jmeter-plugins/
#&& cd /jmeter-plugins/ \
# && wget https://jmeter-plugins.org/downloads/file/JMeterPlugins-ExtrasLibs-1.4.0.zip \
# && unzip -o JMeterPlugins-ExtrasLibs-1.4.0.zip -d /jmeter/apache-jmeter-3.1/

# RUN wget https://jmeter-plugins.org/files/packages/${RANDOM_CSV_FILE} \
#   && unzip ${RANDOM_CSV_FILE} \
#   && cp lib/ext/jmeter-plugins-random-csv-data-set-${RANDOM_CSV_VERSION}.jar ${JMETER_PLUGINS_FOLDER} \
#   && cp lib/ext/jmeter-plugins-manager-1.6.jar ${JMETER_PLUGINS_FOLDER} \
#   && rm ${RANDOM_CSV_FILE}

# Settingt Jmeter Home
ENV JMETER_HOME /jmeter/${JMETER_FILE_PATH}/
# Finally Adding Jmeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH