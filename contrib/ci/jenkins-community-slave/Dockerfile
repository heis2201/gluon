FROM gluonmesh/build:latest

USER root

# this is needed to install default-jre-headless in debian slim images
RUN mkdir -p /usr/share/man/man1
 
RUN apt-get update && apt-get install -y default-jre-headless curl python3 python3-pip python3-sphinx git
RUN pip3 install jenkins-webapi sphinx_rtd_theme
 
# Get docker-compose in the agent container
RUN mkdir -p /home/jenkins
RUN mkdir -p /var/lib/jenkins
RUN mkdir -p /remoting
RUN chown gluon /home/jenkins
RUN chown gluon /var/lib/jenkins
RUN chown gluon /remoting
 
# Start-up script to attach the slave to the master
ADD slave.py /var/lib/jenkins/slave.py

USER gluon
 
WORKDIR /home/jenkins

ENV JENKINS_URL "https://build.ffh.zone/"
ENV JENKINS_SLAVE_ADDRESS ""
ENV SLAVE_EXECUTORS "1"
ENV SLAVE_LABELS "docker"
ENV SLAVE_WORING_DIR ""
ENV CLEAN_WORKING_DIR "true"
 
CMD [ "python3", "-u", "/var/lib/jenkins/slave.py" ]
