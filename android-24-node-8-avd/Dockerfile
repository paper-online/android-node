FROM paperonline/android-node:android-24-node-8

# create virtual device
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "emulator" "system-images;android-${ANDROID_TARGET_SDK_VERSION};default;armeabi-v7a" && \
    ${ANDROID_HOME}/tools/bin/avdmanager create avd -n pixel -d pixel -k "system-images;android-${ANDROID_TARGET_SDK_VERSION};default;armeabi-v7a"

# start adb and connect virtual device
CMD ${ANDROID_HOME}/platform-tools/adb start-server && \
    ${ANDROID_HOME}/tools/emulator -avd pixel -noaudio -no-window
