# Build a Minecraft server on Debian Stable
#
# To run the server:
#
# $ sudo docker run --detach --publish 25565:25565 \
#               --volume /path/to/my/world:/minecraft/world \
#               --name minecraft mbarnes/minecraft

FROM mbarnes/jre
MAINTAINER Matthew Barnes <mbarnes@redhat.com>

# Set the timezone.
ENV TZ US/Eastern
RUN ln --symbolic --no-dereference --force /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone

# Create a user for the Minecraft server.
ENV UID 1000
ENV GID 1000
RUN groupadd --gid $GID minecraft
RUN useradd --uid $UID --gid $GID --home-dir /minecraft --create-home minecraft

# Download the server JAR from Mojang.
RUN apt-get update && apt-get install --assume-yes wget
RUN wget --directory-prefix=/minecraft --no-verbose \
    https://launcher.mojang.com/v1/objects/3737db93722a9e39eeada7c27e7aca28b144ffa7/server.jar

# Copy the server configuration.
COPY --chown=minecraft *.txt server.properties /minecraft/

# Use Minecraft's default server port.
EXPOSE 25565

# Mount a data volume at /minecraft/world to store world data,
# otherwise the world will be lost along with the container.
VOLUME ["/minecraft/world"]

USER minecraft
WORKDIR /minecraft

CMD ["/usr/bin/java", "-Xms512M", "-Xmx512M", "-jar", "server.jar", "nogui"]

