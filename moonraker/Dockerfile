FROM balenalib/raspberrypi3:bullseye

ENV DOCKER=true

RUN apt-get update && \
    apt-get install -y git

# create workdir
RUN mkdir /moonraker
WORKDIR /moonraker

RUN git clone https://github.com/spomjaksilp/moonraker.git

#RUN git clone https://github.com/spomjaksilp/moonraker.git && \
#    ./moonraker/scripts/install-moonraker.sh
