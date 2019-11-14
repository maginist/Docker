FROM ubuntu

RUN apt-get update && \
		apt-get upgrade -y && DEBIAN_frontend=noninteractive && \
		apt-get install -y ca-certificates openssh-server apt-transport-https postfix curl

# install tuto gitlab official website https://about.gitlab.com/install/#ubuntu
# DEBIAN_frontend=noninteractive for skip install interaction https://askubuntu.com/questions/909277/avoiding-user-interaction-with-tzdata-when-installing-certbot-in-a-docker-contai

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
WORKDIR ./
RUN curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh

#LO in case the file url have moved and to output in a file

RUN bash script.deb.sh
RUN apt-get update && apt-get install gitlab-ce
RUN apt update && apt install -y tzdata
RUN useradd gitlab
EXPOSE 443 80 22
RUN echo "root:123456" | chpasswd
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
CMD /opt/gitlab/embedded/bin/runsvdir-start & service ssh start && \
	gitlab-ctl reconfigure && tail -f /dev/null

# https://gitlab.com/gitlab-org/omnibus-gitlab/issues/4257

# docker build -t ex03 .
# docker run -it -p 443:443 -p 80:80 -p 21:22 --privileged ex03
# connect to the address http://(ip Char) with no port
# Mettre sa clé rsa dans les settings site gitlab
# user de base : root mdp : 123456
# pour tester ssh clone : gcl ssh://git@IP:21/root/test.git
