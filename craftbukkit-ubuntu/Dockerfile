FROM ubuntu:utopic
# FROM ubuntu
# trusty ("14.04, Trusty Tahr")
# utopic ("14.10", "Utopic Unicorn" )

MAINTAINER Nico De Ceulaer <nicodeceulaer@gmail.com>

RUN echo -e "\n\n\033[32;1m###############################################################\n\033[32;1m##\n\033[32;1m## \033[33;1mBUKKIT MINECRAFT SERVER\n\033[32;1m##\n\033[32;1m###############################################################\n\n\033[37;0m"


RUN echo -e "\n\n\033[37;1m  * \033[33;1mAdding Universe to sources.list\033[37;0m"

RUN echo "deb http://archive.ubuntu.com/ubuntu utopic main universe" > /etc/apt/sources.list
RUN apt-get update
# RUN apt-get upgrade -y

RUN echo -e "\n\n\033[37;1m  * \033[33;1mAdding webupd8team PPA for Java\033[37;0m"

RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:webupd8team/java -y

RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

RUN apt-get install -y git curl oracle-java7-installer

RUN apt-get install -y wget unzip

RUN echo -e "\n\n\033[37;1m  * \033[33;1mDownloading Bukkit Server\033[37;0m"
RUN mkdir -p /opt/minecraft

# I know, it's spigot, not craftbukkit
# too lazy to update the rest of the script so chaning the name to craftbukkit.jar anyway
RUN wget -O /opt/minecraft/spigot1649.jar http://spigotmc.info/spigot1649.jar
RUN wget -O /opt/minecraft/SpigotPatcher.jar   http://getspigot.org/download/patcher/1.0/SpigotPatcher.jar
RUN wget -O /opt/minecraft/patch.bps   http://www.spigotmc.org/spigot-updates/spigot-20141113a.bps
RUN java -jar /opt/minecraft/SpigotPatcher.jar /opt/minecraft/spigot1649.jar /opt/minecraft/patch.bps /opt/minecraft/spigot.jar

# RUN wget -O /opt/minecraft/craftbukkit.jar http://ci.md-5.net/job/Spigot/lastSuccessfulBuild/artifact/Spigot-Server/target/spigot.jar
##### 2014-11-26 ::
# RUN wget -O /opt/minecraft/craftbukkit.jar http://dl.bukkit.org/latest-rb/craftbukkit.jar
##### 2014-08-20 :: 1.7.9
# RUN wget -O /opt/minecraft/craftbukkit.jar http://cbukk.it/craftbukkit-beta.jar
##### 2014-08-20 :: 1.6.4
# RUN wget -O /opt/minecraft/craftbukkit.jar http://dl.bukkit.org/latest-rb/craftbukkit.jar

ADD server.properties /opt/minecraft/

# To add someone to it, use /op <ExactPlayerName>.
# To remove someone from it, use /deop <ExactPlayerName>
# Server operaters get to use commands like /gamemode and /ban and stuff like that
ADD ops.txt /opt/minecraft/

RUN touch /opt/minecraft/white-list.txt

# 01:27:20 [WARNING] server.properties does not exist
# 01:27:22 [WARNING] Failed to load operators list: java.io.FileNotFoundException: ./ops.txt (No such file or directory)
# 01:27:22 [WARNING] Failed to load white-list: java.io.FileNotFoundException: ./white-list.txt (No such file or directory)

RUN echo -e "\n\n\033[37;1m  * \033[33;1mAdding Plugins \033[37;1m25565 \033[37;0m"

RUN mkdir -p /opt/minecraft/plugins
RUN wget -O /opt/minecraft/plugins/Essentials.zip       http://dev.bukkit.org/media/files/780/922/Essentials.zip
RUN wget -O /opt/minecraft/plugins/Essentials-extra.zip http://dev.bukkit.org/media/files/780/921/Essentials-extra.zip
RUN unzip -d /opt/minecraft/plugins -j /opt/minecraft/plugins/Essentials.zip
RUN unzip -d /opt/minecraft/plugins -j /opt/minecraft/plugins/Essentials-extra.zip

RUN echo -e "\n\n\033[37;1m  * \033[33;1mExposing Port \033[37;1m25565 \033[37;0m"

EXPOSE 25565

WORKDIR /opt/minecraft

# ln -s craftbukkit.jar minecraft_server.jar
RUN ln -s spigot.jar minecraft_server.jar 

RUN mkdir data
RUN  echo "eula=true" > data/eula.txt
RUN  echo "eula=true" > eula.txt

CMD echo -e "\n\n\033[32;1m###############################################################\n\033[32;1m##\n\033[32;1m## \033[33;1mBUKKIT MINECRAFT SERVER\n\033[32;1m##\n\033[32;1m###############################################################\n\n\033[37;0m"
CMD echo -e "\n\n\033[37;1m  * \033[33;1mStarting Minecraft Server \033[37;1m... \033[37;0m"
CMD (cd /opt/minecraft && java -Xmx1024M -Xms768M -jar minecraft_server.jar nogui)

