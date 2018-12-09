FROM ubuntu:18.04
ADD https://builds.cuberite.org/job/Cuberite%20Linux%20x64%20Master/lastSuccessfulBuild/artifact/Cuberite.tar.gz /tmp/
RUN apt-get update -qq && \
    apt-get install -y dumb-init && \
    tar xvzf /tmp/Cuberite.tar.gz -C / && \
    mv /Server /cuberite && \
    rm -rf /tmp/* /var/lib/apt/lists/*
WORKDIR /cuberite/
EXPOSE 8080 25565
VOLUME ["/cuberite/webadmin", "/cuberite/world", "/cuberite/world_nether", "/cuberite/world_the_end"]
ENTRYPOINT ["/usr/bin/dumb-init","/cuberite/Cuberite"]