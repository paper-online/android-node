FROM paperonline/android-node:android-28-node-10

# set timezone
RUN ln -snf /usr/share/zoneinfo/UTC /etc/localtime && echo UTC > /etc/timezone && \
    # update apt-get
    apt-get update -y && \
    # install zip
    apt-get install -y --no-install-recommends zip && \
    # install jq
    apt-get install -y --no-install-recommends jq && \
    # install python
    apt-get install -y --no-install-recommends python-pip python-setuptools && \
    pip install wheel && \
    # install aws cli
    pip install awscli && \
    # clear out caches
    rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/*

USER node
