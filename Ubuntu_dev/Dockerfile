FROM ubuntu:20.04

########### DEVELOPMENT TOOLS ###############
COPY packages /tmp/packages
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qq \
&& apt-get upgrade -y  \
&& apt-get install -y apt-utils \
&& apt-get install -y --no-install-recommends openssh-server xauth \
&& apt-get install -y --no-install-recommends $(cat /tmp/packages) \
&& ln -sf /usr/share/zoneinfo/US/Eastern /etc/localtime \
&& localedef -i en_US -f UTF-8 en_US.UTF-8 \
&& rm -rf /packages /var/lib/apt/lists/*

########## ENABLE SSHD ########################
#
RUN mkdir /var/run/sshd \
&& sed -ri 's/#X11UseLocalhost yes/X11UseLocalhost no/' /etc/ssh/sshd_config  \
&& sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
&& sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
#
EXPOSE 22
#############################################

###########################################


####### Setup the HPS User ##################

COPY passwords.txt /tmp/passwords
RUN adduser hps --shell /bin/bash --system --disabled-password \
&& chpasswd < /tmp/passwords.txt 
COPY .bashrc .profile  /home/hps/

###########################################

CMD ["/usr/sbin/sshd","-D"]




