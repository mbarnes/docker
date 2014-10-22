# Build a Minecraft server on Debian Stable
FROM mbarnes/jre
MAINTAINER Matthew Barnes <mbarnes@redhat.com>

# Minecraft's default server port
EXPOSE 25565

COPY *.jar *.txt server.properties /root/

VOLUME ["/root/world"]

WORKDIR /root

CMD ["/usr/bin/java", "-Xms512M", "-Xmx512M", "-jar", "minecraft_server.1.8.jar", "nogui"]

