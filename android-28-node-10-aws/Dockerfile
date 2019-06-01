FROM paperonline/android-node:android-28-node-10

ENV AWS_ACCESS_KEY=
ENV AWS_SECRET_KEY=
ENV AWS_REGION=

# add aws config
RUN yarn global add @aws-amplify/cli

# run using env config
CMD mkdir ~/.aws && \
    echo "[ci]\naws_access_key_id = $AWS_ACCESS_KEY\naws_secret_access_key = $AWS_SECRET_KEY" > ~/.aws/credentials && \
    echo "[profile ci]\nregion = $AWS_REGION" > ~/.aws/config
