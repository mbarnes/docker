# Build a Minecraft server on Debian Stable
#
# To run the server:
#
# $ sudo docker run --detach --publish 25565:25565 \
#               --volume /path/to/my/world:/root/world \
#               --name minecraft mbarnes/minecraft

FROM mbarnes/jre
MAINTAINER Matthew Barnes <mbarnes@redhat.com>

# Download the server from Amazon S3.
RUN apt-get update && apt-get install -y wget
RUN wget https://s3.amazonaws.com/Minecraft.Download/versions/1.8/minecraft_server.1.8.jar

# Copy server configuration.
COPY *.txt server.properties /root/

# Use Minecraft's default server port.
EXPOSE 25565

# Mount a data volume at /root/world to store world data,
# otherwise the world will be lost along with the container.
VOLUME ["/root/world"]

WORKDIR /root

CMD ["/usr/bin/java", "-Xms512M", "-Xmx512M", "-jar", "minecraft_server.1.8.jar", "nogui"]

