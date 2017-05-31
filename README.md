Dockerfiles for Simbi
=====================

This is an open repository for Dockerfiles used in deployment and in CI. This
repository should contain no secrets.

## Building

To manually build a docker image and push to the docker repository

```shell
cd ./elasticsearch
docker build -t $(cat repository) .
docker push $(cat repository)
```
