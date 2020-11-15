# This is a modified version of the original Dokerfile from https://github.com/KevinOConnor/klipper

# Note that the host still needs to run Linux to connect the printers serial port to
# the container.
# When running, the serial port of your printer should be connected, including an
# argument such as:
#       --device /dev/ttyUSB0:/dev/ttyUSB0
# It's also required that your control program (eg: OctoPrint) be included in the same
# container as Docker does not allow sharing of the virtual serial port outside the
# container.
# The config should be in a file named "printer.cfg" in a directory mounted at:
#       /home/klippy/.config/
# For more Dockerfile examples with Klipper (and Octoprint) see:
# https://github.com/sillyfrog/OctoPrint-Klipper-mjpg-Dockerfile

FROM balenalib/raspberrypi3:bullseye

RUN apt-get update && \
    apt-get install -y sudo git

# Create user
RUN useradd -ms /bin/bash klippy && adduser klippy dialout
USER klippy

#This fixes issues with the volume command setting wrong permissions
RUN mkdir /home/klippy/.config
VOLUME /home/klippy/.config

### Klipper setup ###
WORKDIR /home/klippy

RUN git clone https://github.com/KevinOConnor/klipper.git

USER root
RUN echo 'klippy ALL=(ALL:ALL) NOPASSWD: ALL' > /etc/sudoers.d/klippy && \
    chown klippy:klippy -R klipper
# This is to allow the install script to run without error
RUN ln -s /bin/true /bin/systemctl
USER klippy
RUN ./klipper/scripts/install-debian.sh
# Clean up install script workaround
RUN sudo rm -f /bin/systemctl

# directories for mainsail
RUN mkdir /home/klipper/klipper_config && \
    mkdir /home/klipper/sdcard

CMD ["/home/klippy/klippy-env/bin/python", "/home/klippy/klipper/klippy/klippy.py", "/home/klippy/klipper_config/printer.cfg", "-l", "/tmp/klippy.log", "-a", "/tmp/klippy_uds"]



