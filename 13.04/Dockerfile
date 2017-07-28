FROM       ubuntu:13.04
MAINTAINER Aleksandar Diklic "https://github.com/rastasheep"

ARG root_password=root
ARG rsa='ssh-rsa Some/Garbage/Here docker@mygod.be'

RUN apt-get update

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo root:$root_password | chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN echo GatewayPorts clientspecified >> /etc/ssh/sshd_config
RUN mkdir -p /root/.ssh
RUN echo $rsa > /root/.ssh/authorized_keys

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
