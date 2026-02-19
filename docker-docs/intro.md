---
sidebar_position: 1
slug: /
---

### Docker

- create container:

docker create container create container but not start them.

```
docker container create <image name>
docker container create hello-world
```

- to see list of active container running:

```
docker ps
```

- to see all created container list:

```
docker ps --all
```

- to start container:

```
docker container start <container id>
docker container start 990f0ee6c080a48b0190268541913ca8e72f3f3fb9b302a425edefc999e22474

docker container start --attach 990f0ee6c080a48b0190268541913ca8e72f3f3fb9b302a425edefc999e22474
```

- another way to create and start container:

docker run create container then start container and add the --attach to get proper success msg.

```
docker run hello-world
```
