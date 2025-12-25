FROM ros:humble

ARG USERNAME=QuadTech
ARG USER_UID=1003
ARG USER_GID=1003

RUN if getent passwd ${USER_UID}; then userdel -r $(getent passwd ${USER_UID} | cut -d: -f1); fi

RUN groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
    && apt-get update \
    && apt-get install -y sudo \
    && echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

RUN apt-get update && apt-get install -y \
    python3-pip \
    wget \
    curl \
    mesa-utils \
    libgl1-mesa-dri \
    libgl1-mesa-glx \
    x11-apps \
    dbus-x11 \
    ros-humble-rviz2 \
    && rm -rf /var/lib/apt/lists/*

ENV SHELL=/bin/bash
ENV LD_LIBRARY_PATH=/opt/ros/humble/opt/rviz_ogre_vendor/lib:$LD_LIBRARY_PATH

RUN echo "source /opt/ros/humble/setup.bash" >> /home/${USERNAME}/.bashrc \
 && echo "export LD_LIBRARY_PATH=/opt/ros/humble/opt/rviz_ogre_vendor/lib:\$LD_LIBRARY_PATH" >> /home/${USERNAME}/.bashrc

USER ${USERNAME}
WORKDIR /home/${USERNAME}

CMD ["/bin/bash"]
