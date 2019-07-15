# couldn't have done it without these guys
# https://github.com/thyrlian/AndroidSDK
# https://github.com/alvr/alpine-android

FROM ubuntu:18.04

# set args
ARG NODE_VERSION=10.16.0
ARG GRADLE_VERSION=5.1.1
ARG KOTLIN_VERSION=1.3.21
ARG ANDROID_SDK_VERSION=4333796
ARG ANDROID_BUILD_TOOLS_VERSION=28.0.3
ARG ANDROID_TARGET_SDK_VERSION=28

# set env vars
ENV ANDROID_TARGET_SDK_VERSION ${ANDROID_TARGET_SDK_VERSION}
ENV ANDROID_HOME /opt/android-sdk
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV GRADLE_HOME /opt/gradle
ENV KOTLIN_HOME /opt/kotlinc
ENV PATH ${PATH}:${GRADLE_HOME}/bin:${KOTLIN_HOME}/bin:${ANDROID_HOME}/emulator:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools/bin
ENV _JAVA_OPTIONS -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap
# workaround for issue https://issuetracker.google.com/issues/37137213
ENV LD_LIBRARY_PATH ${ANDROID_HOME}/emulator/lib64:${ANDROID_HOME}/emulator/lib64/qt/lib

# support multiarch: i386 architecture
RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    # install libs, java and qt
    apt-get install -y --no-install-recommends curl && \
    apt-get install -y --no-install-recommends libncurses5:i386 libc6:i386 libstdc++6:i386 lib32gcc1 lib32ncurses5 lib32z1 zlib1g:i386 && \
    apt-get install -y --no-install-recommends git wget unzip && \
    apt-get install -y --no-install-recommends openjdk-8-jdk && \
    apt-get install -y --no-install-recommends qt5-default && \
    # add node user
    addgroup --gid 1000 node && \
    adduser --uid 1000 --gid 1000 --shell /bin/sh node && \
    # install node
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get update -y && \
    apt-get install -y --no-install-recommends nodejs=${NODE_VERSION}* && \
    npm install -g yarn && \
    # install gradle
    cd /opt && \
    wget -q https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip gradle*.zip && \
    ls -d */ | sed 's/\/*$//g' | xargs -I{} mv {} gradle && \
    rm gradle*.zip && \
    # install kotlin compiler
    cd /opt && \
    wget -q https://github.com/JetBrains/kotlin/releases/download/v${KOTLIN_VERSION}/kotlin-compiler-${KOTLIN_VERSION}.zip && \
    unzip *kotlin*.zip && \
    rm *kotlin*.zip && \
    # install android sdk
    mkdir -p ${ANDROID_HOME} && cd ${ANDROID_HOME} && \
    wget -q https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_VERSION}.zip && \
    unzip *tools*linux*.zip && \
    rm *tools*linux*.zip && \
    # install android sdk packages
    mkdir -p ~/.android/ && touch ~/.android/repositories.cfg && \
    yes | ${ANDROID_HOME}/tools/bin/sdkmanager "--licenses" && \
    ${ANDROID_HOME}/tools/bin/sdkmanager "--update" && \
    ${ANDROID_HOME}/tools/bin/sdkmanager "platform-tools" "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" "platforms;android-${ANDROID_TARGET_SDK_VERSION}" && \
    # clear out caches
    rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/*

# set permissions on /opt
RUN mkdir -p /opt/atlassian/pipelines/agent/build && \
    chown -R node:node /opt
