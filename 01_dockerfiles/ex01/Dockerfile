FROM debian

EXPOSE 9987/udp
EXPOSE 10011
EXPOSE 30033

RUN useradd maginist

WORKDIR /home/maginist
RUN apt-get update -y && apt-get upgrade -y && apt-get install wget bzip2 -y
RUN wget https://files.teamspeak-services.com/releases/server/3.9.1/teamspeak3-server_linux_amd64-3.9.1.tar.bz2
RUN tar xfv teamspeak3-server_linux_amd64-3.9.1.tar.bz2
WORKDIR teamspeak3-server_linux_amd64
RUN touch .ts3server_license_accepted
ENTRYPOINT ["sh", "ts3server_minimal_runscript.sh"]

#docker build -t ex01 .
#docker run -it -p 9987:9987/udp -p 10011:10011 -p 30033:30033 --rm ex01

