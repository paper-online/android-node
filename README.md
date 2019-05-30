# Deploying a new image

```bash
docker build ./android-24-node-8/
docker tag 3e122a1fe26e paperonline/android-node:android-24-node-8
docker login
docker push paperonline/android-node:android-24-node-8
```