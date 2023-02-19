FROM tomcat:9.0

COPY first.war $CATALINA_HOME
RUN mkdir -p $CATALINA_HOME/webapps/ROOT
COPY index.html $CATALINA_HOME/webapps/ROOT
RUN mkdir $CATALINA_HOME/webapps/first
RUN cd $CATALINA_HOME/webapps/first ; jar xvf $CATALINA_HOME/first.war
RUN sed -i -e "s/~\/book/\/opt\/h2\/data\/hokkaido/" $CATALINA_HOME/webapps/first/META-INF/context.xml
RUN sed -i -e "s/localhost/h2db/" $CATALINA_HOME/webapps/first/META-INF/context.xml
CMD ["catalina.sh", "run"]
