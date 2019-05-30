# Deploying a new image

```bash
docker build ./android-24-node-10-avd/
docker tag b916ba731127 paperonline/android-node:android-24-node-10-avd
docker login
docker push paperonline/android-node:android-24-node-10-avd
```