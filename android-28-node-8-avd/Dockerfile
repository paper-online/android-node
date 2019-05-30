FROM paperonline/android-node:android-28-node-8

# set exposed port for adb
EXPOSE 5037

# create virtual device
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "emulator" "system-images;android-${ANDROID_TARGET_SDK_VERSION};google_apis_playstore;x86_64" && \
    ${ANDROID_HOME}/tools/bin/avdmanager create avd -n pixel -d pixel -k "system-images;android-${ANDROID_TARGET_SDK_VERSION};google_apis_playstore;x86_64"

# start adb and connect virtual device
CMD ${ANDROID_HOME}/platform-tools/adb start-server && \
    ${ANDROID_HOME}/emulator/emulator-headless -avd pixel -no-audio -no-accel -no-window -gpu off
