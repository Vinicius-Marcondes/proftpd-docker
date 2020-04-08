FROM debian:9-slim

LABEL com.version='1.0' com.maintainer='Vinicius Marcondes (Vinicius-Marcondes on Github)' 

RUN apt-get update -qq && \
	apt-get install -y proftpd openssh-server && \
	apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN sed -i "s/# DefaultRoot/DefaultRoot/" /etc/proftpd/proftpd.conf

EXPOSE 22 

ADD docker-entrypoint.sh /usr/local/sbin/docker-entrypoint.sh
#ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]

CMD ["/usr/local/sbin/docker-entrypoint.sh"] 
#proftpd", "--nodaemon"]