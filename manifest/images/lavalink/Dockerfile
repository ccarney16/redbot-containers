FROM docker.io/library/openjdk:11-slim-bullseye

ARG VERSION

RUN apt update && \
    apt install -y libmpg123-0 curl

# Run as non-root user
RUN groupadd -g 322 lavalink && \
    useradd -r -u 322 -g lavalink lavalink

RUN mkdir /app && cd /app && \
    curl -LO https://github.com/Cog-Creators/Lavalink-Jars/releases/download/${VERSION}/Lavalink.jar

WORKDIR /config
USER lavalink

ENTRYPOINT ["java", "-Djdk.tls.client.protocols=TLSv1.1,TLSv1.2", "-Xmx4G", "-jar", "/app/Lavalink.jar"]