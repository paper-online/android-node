FROM paperonline/android-node:android-24-node-10

RUN sdkmanager "system-images;android-24;google_apis;x86" \
    && android create avd -n pixel -d pixel -k "system-images;android-24;google_apis;x86"
