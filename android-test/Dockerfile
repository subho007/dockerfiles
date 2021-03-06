FROM ubuntu:12.04

MAINTAINER alexfu

RUN apt-get update -qq

# Dependencies to execute android
RUN apt-get install -y --no-install-recommends openjdk-7-jdk ia32-libs ia32-libs-multiarch git ssh

# Main Android SDK
RUN apt-get install -y --no-install-recommends wget
RUN cd /opt && wget -q http://dl.google.com/android/android-sdk_r22.6.2-linux.tgz
RUN cd /opt && tar xzf android-sdk_r22.6.2-linux.tgz
RUN cd /opt && rm -f android-sdk_r22.6.2-linux.tgz

# Other tools and resources of Android SDK
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN echo y | android update sdk -a -u -f -t tools
RUN echo y | android update sdk -a -u -f -t platform-tools
RUN echo y | android update sdk -a -u -f -t build-tools-19.1.0
RUN echo y | android update sdk -a -u -f -t android-19
RUN echo y | android update sdk -a -u -f -t sysimg-19
RUN echo y | android update sdk -a -u -f -t addon-google_apis-google-19
RUN echo y | android update sdk -a -u -f -t extra-google-m2repository
RUN echo y | android update sdk -a -u -f -t extra-android-m2repository

# Cleaning
RUN apt-get clean

# Add AVD
RUN android create avd -n kitkat-arm -t "Google Inc.:Google APIs:19"

# Add helper scripts
ADD start-emulator /usr/local/bin/
ADD wait-for-emulator /usr/local/bin/
RUN chmod +x /usr/local/bin/start-emulator
RUN chmod +x /usr/local/bin/wait-for-emulator
