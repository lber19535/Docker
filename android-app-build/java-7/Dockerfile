FROM java:7

ENV ANDROID_SDK_FILE android-sdk_r24.4.1-linux.tgz
ENV ANDROID_SDK_URL http://dl.google.com/android/${ANDROID_SDK_FILE}
ENV ANDROID_HOME /opt/android-sdk-linux


# Install Deps
RUN dpkg --add-architecture i386 && \
    apt-get -qq update && \
    apt-get -qq install -y curl ant gradle libncurses5:i386 libstdc++6:i386 zlib1g:i386

# Install Android SDK
RUN cd /opt && wget ${ANDROID_SDK_URL} && tar xzvf ${ANDROID_SDK_FILE} && rm -f ${ANDROID_SDK_FILE} && chown -R root.root ${ANDROID_HOME}

# Setup environment
ENV ANDROID_HOME /opt/android-sdk_r24.4.1-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

# Install sdk
RUN echo y | android update sdk --all --no-ui --filter platform-tools,tools,build-tools-21,build-tools-21.0.1,build-tools-21.0.2,build-tools-21.1,build-tools-21.1.1,build-tools-21.1.2,build-tools-22,build-tools-22.0.1,build-tools-23.0.0,build-tools-23.0.3,build-tools-24.0.2,build-tools-24.0.1,build-tools-24,android-22,android-23,android-24,addon-google_apis_x86-google-21,extra-android-support,extra-android-m2repository,extra-google-m2repository,extra-google-google_play_services

RUN which adb
RUN which android

# Install repo
RUN cd /opt && mkdir bin && cd bin && wget https://raw.githubusercontent.com/android/tools_repo/master/repo repo && chmod a+x repo
ENV OPT_BIN /opt/bin
ENV PATH ${PATH}:${OPT_BIN}


# Cleaning
RUN apt-get clean

# GO to workspace
RUN mkdir -p /opt/workspace
WORKDIR /opt/workspace

VOLUME ["/opt/workspace"]