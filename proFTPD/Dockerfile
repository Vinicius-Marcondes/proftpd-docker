FROM debian:9-slim

LABEL version='1.1' 

LABEL maintainer='Vinicius Marcondes (Vinicius-Marcondes on Github)' 

ARG MAIN_USER
ARG MAIN_USER_PASSWORD

ARG FTP_LIST
ENV FTP_LIST=${FTP_LIST}
ARG USERADD_OPTIONS
ENV USERADD_OPTIONS=${USERADD_OPTIONS}

RUN echo "************** install necessary packages **************" && \
	apt-get update -qq && \
	apt-get install -y curl \ 
					   sed \
					   openssl \
					   openssh-server \ 
					   openssh-sftp-server \
					   sudo \
					   logrotate \
					   vim \
					   proftpd && \
	apt-get clean && \
	groupadd ${MAIN_USER} && \
	useradd --shell /bin/sh ${USERADD_OPTIONS} -G ${MAIN_USER} -d /home/${MAIN_USER} --password ${MAIN_USER_PASSWORD} ${MAIN_USER} && \
	\
	echo "************** setup openssh & proftpd enviroment" && \
	# sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config && \
	# sed -i 's/$Port 22/Port 2323/g' /etc/ssh/sshd_config && \
	usermod --shell /bin/bash ${MAIN_USER} && \
	# sed -i "s/# DefaultRoot/DefaultRoot/" /etc/proftpd/proftpd.conf \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 

EXPOSE 22 
EXPOSE 2323

ADD docker-entrypoint.sh /usr/local/sbin/docker-entrypoint.sh
#ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]

CMD ["/usr/local/sbin/docker-entrypoint.sh"] 
#proftpd", "--nodaemon"]