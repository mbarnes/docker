# Build a Minecraft server on Debian Stable
#
# To run the server:
#
# $ sudo docker run --detach --publish 25565:25565 \
#               --volume /path/to/my/world:/root/world \
#               --name minecraft mbarnes/minecraft

FROM mbarnes/jre
MAINTAINER Matthew Barnes <mbarnes@redhat.com>

# Download the server JAR from Mojang.
RUN apt-get update && apt-get install --assume-yes wget
RUN wget --directory-prefix=/root --no-verbose \
    https://launcher.mojang.com/v1/objects/3737db93722a9e39eeada7c27e7aca28b144ffa7/server.jar

# Copy the server configuration.
COPY *.txt server.properties /root/

# Use Minecraft's default server port.
EXPOSE 25565

# Mount a data volume at /root/world to store world data,
# otherwise the world will be lost along with the container.
VOLUME ["/root/world"]

WORKDIR /root

CMD ["/usr/bin/java", "-Xms512M", "-Xmx512M", "-jar", "server.jar", "nogui"]

