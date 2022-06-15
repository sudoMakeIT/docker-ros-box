ARG ros_distro

FROM osrf/ros:${ros_distro}-desktop-full

ARG ros_distro

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get -yq --force-yes install \
	sudo \
	python3-catkin-tools \
	dialog \
	less \
	nano \
	x-window-system \
	mesa-utils


#https://stackoverflow.com/questions/27701930/how-to-add-users-to-docker-container
RUN useradd -rm -d /home/${ros_distro}-dev -s /bin/bash -g root -G sudo -u 1001 -p "$(openssl passwd -6 root)" ${ros_distro}-dev

USER ${ros_distro}-dev

RUN mkdir -p /home/${ros_distro}-dev/catkin_ws/src && \
	mkdir -p /home/${ros_distro}-dev/data && \
	mkdir -p /home/${ros_distro}-dev/tools 

ENV HOME /home/${ros_distro}-dev
COPY bashrc /home/${ros_distro}-dev/.bashrc
COPY bashrc /root/.bashrc
COPY bash_profile /home/${ros_distro}-dev/.bash_profile
COPY bash_profile /root/.bash_profile

COPY rosbox_entrypoint.sh /rosbox_entrypoint.sh
ENTRYPOINT /rosbox_entrypoint.sh
