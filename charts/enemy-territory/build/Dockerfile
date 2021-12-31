FROM ubuntu

WORKDIR /etlegacy

RUN dpkg --add-architecture i386

RUN apt-get update && \
    apt-get install -y \
        curl \
        unzip \
        libc6:i386 \
        wget

RUN mkdir -p /tmp/etsetup && \
    cd /tmp/etsetup && \
    wget https://cdn.splashdamage.com/downloads/games/wet/et260b.x86_full.zip && \
    unzip et260b.x86_full.zip && \
    ./et260b.x86_keygen_V03.run --noexec --target /tmp/etsetup/extracted && \
    mv extracted/* /etlegacy && \
    cd /etlegacy && \
    mv bin/Linux/x86/etded.x86 . && \
    rm -rf /tmp/etsetup

# In order for ETTV relays to connect to your server, replace the ETTV binary from GamesTV and make it executable.
RUN wget https://www.gamestv.org/drop/ettv.x86 && \
    chmod +x ettv.x86

# Download and extract ETPro into place.
RUN wget https://www.gamestv.org/drop/etpro-3_2_6.zip && \
    unzip etpro-3_2_6.zip && \
    rm -rf unzip etpro-3_2_6.zip

COPY server.cfg /etlegacy/etpro/server.cfg

COPY start.sh /etlegacy/start.sh

EXPOSE 27960/udp

ENTRYPOINT [ "/etlegacy/start.sh" ]
