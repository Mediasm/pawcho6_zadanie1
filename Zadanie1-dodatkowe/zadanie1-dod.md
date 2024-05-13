
# pawcho Zadanie 1 dodatkowe

## Table of Contents
- [Build image for linux/arm64 and linux/amd64](#linux/arm64&linux/amd64)
- [Cloning from github & ghcr.io](#ghcr.io)

## Build image for linux/arm64 and linux/amd64

### Modify Dockerfile -> Dockerfile_linux
```
Modified with:

# syntax = docker/dockerfile:1.4
RUN --mount=type=cache,target=/home/node/app/.npm,sharing=locked
```

### Creating builder
```
PS D:\sem6\Docker\zad1> docker buildx use zad1builder                                                   
PS D:\sem6\Docker\zad1> docker buildx ls                                 
zad1builder *    docker-container
  zad1builder0   npipe:////./pipe/docker_engine running v0.13.2  linux/amd64, linux/amd64/v2, linux/amd64/v3, linux/arm64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/mips64le, linux/mips64, linux/arm/v7, linux/arm/v6
default          docker
  default        default                        running v0.12.5  linux/amd64, linux/amd64/v2, linux/amd64/v3, linux/arm64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/mips64le, linux/mips64, linux/arm/v7, linux/arm/v6
desktop-linux    docker
  desktop-linux  desktop-linux                  running v0.12.5  linux/amd64, linux/amd64/v2, linux/amd64/v3, linux/arm64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/mips64le, linux/mips64, linux/arm/v7, linux/arm/v6
PS D:\sem6\Docker\zad1>
```

### Build image

```
docker buildx build   --platform linux/amd64,linux/arm64   --build-arg VERSION='1.0'   --push   --cache-from type=registry,ref=artemsm/zadanie1:v1   --cache-to type=registry,ref=artemsm/zadanie1:v2-linux,mode=max -f Dockerfile_linux   -t artemsm/zadanie1:v2-linux .
```

https://hub.docker.com/layers/artemsm/zadanie1/v2-linux/images/sha256-2190e13a05c2ac2002863ca2f704e1b7529dfd0991a60859bdf49d47a4c7270b?context=repo


## Cloning from github & ghcr.io

### Dockerfile_gh

Add the private SSH key to the container:
```
ARG SSH_PRIVATE_KEY
RUN mkdir -p /root/.ssh && echo "$SSH_PRIVATE_KEY" > /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa
```

Clone the repo with webapp only:
```
RUN git clone https://github.com/Mediasm/zadanie1-app.git
```

https://github.com/Mediasm/zadanie1-app.git


### Build command
```
docker buildx build \
  -f Dockerfile_gh \
  --secret id=ssh,src=.ssh/id_ed25519 \
  --platform linux/amd64,linux/arm64 \
  -t ghcr.io/mediasm/zadanie1:v1-gh \
  --builder zad1builder \
  --push .
```
### Result
```
[+] Building 150.2s (36/36) FINISHED                                                                                                                                                                                                                           docker-container:zad1builder
 => [internal] load build definition from Dockerfile_gh                                                                                                                                                                                                                                0.0s
 => => transferring dockerfile: 1.18kB                                                                                                                                                                                                                                                 0.0s
 => resolve image config for docker-image://docker.io/docker/dockerfile:1.4                                                                                                                                                                                                            1.4s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io                                                                                                                                                                                                                       0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1.4@sha256:9ba7531bd80fb0a858632727cf7a112fbfd19b17e94c4e84ced81e24ef1a0dbc                                                                                                                                                      0.0s
 => => resolve docker.io/docker/dockerfile:1.4@sha256:9ba7531bd80fb0a858632727cf7a112fbfd19b17e94c4e84ced81e24ef1a0dbc                                                                                                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                                                                                                                                                                      0.0s
 => => transferring context: 2B                                                                                                                                                                                                                                                        0.0s
 => [linux/arm64 internal] load metadata for docker.io/library/node:alpine                                                                                                                                                                                                             1.5s
 => [linux/arm64 internal] load metadata for docker.io/alpine/git:latest                                                                                                                                                                                                               1.0s
 => [linux/amd64 internal] load metadata for docker.io/alpine/git:latest                                                                                                                                                                                                               1.5s
 => [linux/amd64 internal] load metadata for docker.io/library/node:alpine                                                                                                                                                                                                             1.2s
 => [auth] library/node:pull token for registry-1.docker.io                                                                                                                                                                                                                            0.0s
 => [auth] alpine/git:pull token for registry-1.docker.io                                                                                                                                                                                                                              0.0s
 => [linux/amd64 builder 1/4] FROM docker.io/library/node:alpine@sha256:916b42f9e83466eb17d60a441a96f5cd57033bbfee6a80eae8e3249f34cf8dbe                                                                                                                                               0.0s
 => => resolve docker.io/library/node:alpine@sha256:916b42f9e83466eb17d60a441a96f5cd57033bbfee6a80eae8e3249f34cf8dbe                                                                                                                                                                   0.0s
 => [linux/amd64 source 1/5] FROM docker.io/alpine/git@sha256:76fdb7210689fc26c6ff101c4adacf9d12d3d25a919a7d8ff42ebaef5bedba65                                                                                                                                                         0.1s
 => => resolve docker.io/alpine/git@sha256:76fdb7210689fc26c6ff101c4adacf9d12d3d25a919a7d8ff42ebaef5bedba65                                                                                                                                                                            0.0s
 => [linux/arm64 source 1/5] FROM docker.io/alpine/git@sha256:76fdb7210689fc26c6ff101c4adacf9d12d3d25a919a7d8ff42ebaef5bedba65                                                                                                                                                         0.0s
 => => resolve docker.io/alpine/git@sha256:76fdb7210689fc26c6ff101c4adacf9d12d3d25a919a7d8ff42ebaef5bedba65                                                                                                                                                                            0.0s
 => [linux/arm64 builder 1/4] FROM docker.io/library/node:alpine@sha256:916b42f9e83466eb17d60a441a96f5cd57033bbfee6a80eae8e3249f34cf8dbe                                                                                                                                               0.1s
 => => resolve docker.io/library/node:alpine@sha256:916b42f9e83466eb17d60a441a96f5cd57033bbfee6a80eae8e3249f34cf8dbe                                                                                                                                                                   0.0s
 => CACHED [linux/amd64 builder 2/4] WORKDIR /app                                                                                                                                                                                                                                      0.0s
 => CACHED [linux/amd64 source 2/5] WORKDIR /app                                                                                                                                                                                                                                       0.0s
 => CACHED [linux/amd64 source 3/5] RUN mkdir -p /root/.ssh && echo "$SSH_PRIVATE_KEY" > /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa                                                                                                                                              0.0s
 => CACHED [linux/amd64 source 4/5] RUN ssh-keyscan github.com >> /root/.ssh/known_hosts                                                                                                                                                                                               0.0s 
 => CACHED [linux/amd64 source 5/5] RUN git clone https://github.com/Mediasm/zadanie1-app.git                                                                                                                                                                                          0.0s 
 => CACHED [linux/amd64 builder 3/4] COPY --from=source /app/zadanie1-app /app                                                                                                                                                                                                         0.0s 
 => CACHED [linux/amd64 builder 4/4] RUN npm install                                                                                                                                                                                                                                   0.0s 
 => CACHED [linux/amd64 stage-2 3/4] COPY --from=builder /app /app                                                                                                                                                                                                                     0.0s 
 => CACHED [linux/amd64 stage-2 4/4] RUN echo "Server started on $(date) by Artem Smolii, listening on port 5000"                                                                                                                                                                      0.0s 
 => CACHED [linux/arm64 builder 2/4] WORKDIR /app                                                                                                                                                                                                                                      0.0s 
 => CACHED [linux/arm64 source 2/5] WORKDIR /app                                                                                                                                                                                                                                       0.0s 
 => CACHED [linux/arm64 source 3/5] RUN mkdir -p /root/.ssh && echo "$SSH_PRIVATE_KEY" > /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa                                                                                                                                              0.0s 
 => CACHED [linux/arm64 source 4/5] RUN ssh-keyscan github.com >> /root/.ssh/known_hosts                                                                                                                                                                                               0.0s 
 => CACHED [linux/arm64 source 5/5] RUN git clone https://github.com/Mediasm/zadanie1-app.git                                                                                                                                                                                          0.0s 
 => CACHED [linux/arm64 builder 3/4] COPY --from=source /app/zadanie1-app /app                                                                                                                                                                                                         0.0s 
 => CACHED [linux/arm64 builder 4/4] RUN npm install                                                                                                                                                                                                                                   0.0s 
 => CACHED [linux/arm64 stage-2 3/4] COPY --from=builder /app /app                                                                                                                                                                                                                     0.0s 
 => CACHED [linux/arm64 stage-2 4/4] RUN echo "Server started on $(date) by Artem Smolii, listening on port 5000"                                                                                                                                                                      0.0s 
 => exporting to image                                                                                                                                                                                                                                                               146.9s 
 => => exporting layers                                                                                                                                                                                                                                                                0.0s 
 => => exporting manifest sha256:9f1c347d5bc4d02cb4d86c2ad26c8602fe2b7a6a19edc0fca42ce4f2a0600d6a                                                                                                                                                                                      0.0s 
 => => exporting config sha256:447bc61c88b7cde5fd7caa7922cf3c3c3db0be291b5431fb7685d0653167701f                                                                                                                                                                                        0.0s 
 => => exporting attestation manifest sha256:33b4b67754ae6dd87af226440f628bccf280a3828b06417efbce738a3d127125                                                                                                                                                                          0.0s 
 => => exporting manifest sha256:71e86fe64d8e340366251b3aa3aa9b5ec84eeee13aba80a0b9c08fa1b8f61805                                                                                                                                                                                      0.0s 
 => => exporting config sha256:dfd834c95d71e0c0eebb887eaaae646f6da53ebc2fc3ec9f99a6943d9715478d                                                                                                                                                                                        0.0s 
 => => exporting attestation manifest sha256:f2166b46f66a23a54800a145c61a5c291643f51cd57d18df18a189b26ab4e3dc                                                                                                                                                                          0.0s 
 => => exporting manifest list sha256:b762df02fb5023d79c1637d26eae8838857e39cd5479a7754d903577bf2abf05                                                                                                                                                                                 0.0s 
 => => pushing layers                                                                                                                                                                                                                                                                143.1s 
 => => pushing manifest for ghcr.io/mediasm/zadanie1:v1-gh@sha256:b762df02fb5023d79c1637d26eae8838857e39cd5479a7754d903577bf2abf05                                                                                                                                                     3.7s 
 => [auth] mediasm/zadanie1:pull,push token for ghcr.io                                                                                                                                                                                                                                0.0s 
 => [auth] mediasm/zadanie1:pull,push token for ghcr.io                    
```

### Package on github

https://github.com/users/Mediasm/packages/container/package/zadanie1

 ### Container command
```
 Administrator@NexusLite-PC MINGW64 /d/sem6/Docker/zad1 (master)
$ docker run -d --name my-webapp -p 5000:5000 ghcr.io/mediasm/zadanie1:v1-gh
Unable to find image 'ghcr.io/mediasm/zadanie1:v1-gh' locally
v1-gh: Pulling from mediasm/zadanie1
4abcf2066143: Already exists                                                                                                                                                                                                                                                                
bc27026fefda: Already exists                                                                                                                                                                                                                                                                
a095e3dd9985: Already exists                                                                                                                                                                                                                                                                
4f900f06de16: Already exists                                                                                                                                                                                                                                                                
119918fb3d67: Pull complete
dade790a6cca: Pull complete
4f4fb700ef54: Pull complete
Digest: sha256:b762df02fb5023d79c1637d26eae8838857e39cd5479a7754d903577bf2abf05
Status: Downloaded newer image for ghcr.io/mediasm/zadanie1:v1-gh
556d0fd677f60f94bcd7f4d9f32c864be22d92172516a5bd6a7ed4414daf10bb
```
### Logs

```
Administrator@NexusLite-PC MINGW64 /d/sem6/Docker/zad1 (master)
$ docker logs my-webapp
Server started on port 5000. Author: Artem Smolii.
```

### Screens