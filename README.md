# Deploying a new image

```bash
docker build ./android-24-node-8/
docker tag f1e4e4d347d3 paperonline/android-node:android-24-node-8
docker login
docker push paperonline/android-node:android-24-node-8
```