# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.241.1/containers/java/.devcontainer/base.Dockerfile
FROM ubuntu:focal

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

# Create the user
RUN apt-get update \
    && apt-get install -y sudo \
    && groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
 
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y openjdk-8-jdk wget maven git nano curl \
    && INSTALL_LOCATION='/opt/android-studio' \
    && LATEST_VERSION='2021.2.1.16' \
    && mkdir $INSTALL_LOCATION $INSTALL_LOCATION/download \
# make the vscode user the owner
    && chown -R 1000:1000 $INSTALL_LOCATION \
    && cd $INSTALL_LOCATION/download \
    && wget https://dl.google.com/dl/android/studio/ide-zips/$LATEST_VERSION/android-studio-$LATEST_VERSION-linux.tar.gz \
    && echo "after wget" \
    && zcat $INSTALL_LOCATION/download/android-studio-$LATEST_VERSION-linux.tar.gz | tar xvf - \
    && echo "after zcat" \
    && mv android-studio/* $INSTALL_LOCATION \
    && echo "after move" \
    && cd $INSTALL_LOCATION \
    && rm -rf $INSTALL_LOCATION/download \
    && echo "after rm" \
    && echo "ANDROID_SDK_ROOT=/opt/android-studio/" | tee -a /etc/environment \
    && echo "after tee" \
    && echo "ANDROID_SDK_ROOT=/opt/android-studio/bin" | tee -a /etc/environment \
    && touch /etc/profile.d/10-set-env.sh \
    && echo "export ANDROID_SDK_ROOT=/opt/android-studio/" | tee -a /etc/profile.d/10-set-env.sh \
    && update-java-alternatives --set /usr/lib/jvm/java-1.8.0-openjdk-amd64 \
    && echo "export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64" | tee -a /etc/profile.d/10-set-env.sh \
    && export JDK_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64

RUN usermod --shell /bin/bash vscode

USER $USERNAME

RUN sudo apt-get install -y curl \
    && curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash


    


