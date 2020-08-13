# Centos based container with Java and Tomcat
FROM centos:7
MAINTAINER mohanraz@gmail.com

# Install prepare infrastructure
RUN yum -y update
RUN yum -y install wget tar java-1.8.0-openjdk

# Prepare environment 
ENV CATALINA_HOME /opt/tomcat 
ENV PATH $PATH:$CATALINA_HOME/bin:$CATALINA_HOME/scripts



RUN wget http://archive.apache.org/dist/tomcat/tomcat-7/v7.0.61/bin/apache-tomcat-7.0.61.tar.gz && \
 tar -xvf apache-tomcat-7.0.61.tar.gz && \
 rm apache-tomcat*.tar.gz && \
 mv apache-tomcat* ${CATALINA_HOME}

RUN chmod +x ${CATALINA_HOME}/bin/*sh

# Create Tomcat admin user
ADD config/create_admin_user.sh $CATALINA_HOME/scripts/create_admin_user.sh
ADD config/tomcat.sh $CATALINA_HOME/scripts/tomcat.sh
RUN chmod +x $CATALINA_HOME/scripts/*.sh

# Create tomcat user
RUN groupadd -r tomcat && \
 useradd -g tomcat -d ${CATALINA_HOME} -s /sbin/nologin  -c "Tomcat user" tomcat && \
 chown -R tomcat:tomcat ${CATALINA_HOME}

WORKDIR /opt/tomcat

EXPOSE 8080
EXPOSE 8009
ADD code/target/java-tomcat-maven-example.war /opt/tomcat/webapps/java-tomcat-maven-example.war

USER tomcat
CMD ["tomcat.sh"]