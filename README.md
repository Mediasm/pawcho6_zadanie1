Commands:
```docker build -t zadanie1_alpine:v1 .
docker run -d -p 5001:5000 --name zadanie1_alpine_v1 zadanie1_alpine:v1
```

Terminal:
```
PS D:\sem6\Docker\zad1> docker build -t zadanie1_alpine:v1 .
[+] Building 1.3s (14/14) FINISHED                                                                                                                                                                                                                                                               docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                                                                                                                       0.0s
 => => transferring dockerfile: 659B                                                                                                                                                                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/node:alpine                                                                                                                                                                                                                                             1.2s
 => [auth] library/node:pull token for registry-1.docker.io                                                                                                                                                                                                                                                0.0s
 => [internal] load .dockerignore                                                                                                                                                                                                                                                                          0.0s
 => => transferring context: 2B                                                                                                                                                                                                                                                                            0.0s
 => [builder 1/7] FROM docker.io/library/node:alpine@sha256:916b42f9e83466eb17d60a441a96f5cd57033bbfee6a80eae8e3249f34cf8dbe                                                                                                                                                                               0.0s
 => [internal] load build context                                                                                                                                                                                                                                                                          0.0s
 => => transferring context: 60B                                                                                                                                                                                                                                                                           0.0s
 => CACHED [builder 2/7] WORKDIR /home/node/app                                                                                                                                                                                                                                                            0.0s
 => CACHED [builder 3/7] COPY package.json ./                                                                                                                                                                                                                                                              0.0s
 => CACHED [builder 4/7] RUN npm install --only=production                                                                                                                                                                                                                                                 0.0s
 => CACHED [builder 5/7] COPY app.js ./                                                                                                                                                                                                                                                                    0.0s
 => CACHED [builder 6/7] RUN cp /usr/local/bin/node /home/node/app/node                                                                                                                                                                                                                                    0.0s
 => CACHED [builder 7/7] RUN chmod +x /home/node/app/node                                                                                                                                                                                                                                                  0.0s
 => CACHED [stage-1 3/3] COPY --from=builder /home/node/app .                                                                                                                                                                                                                                              0.0s
 => exporting to image                                                                                                                                                                                                                                                                                     0.0s
 => => exporting layers                                                                                                                                                                                                                                                                                    0.0s
 => => writing image sha256:561d07c70c426e21af58742b32e7aed18b5a93a32c20679921701e061b224799                                                                                                                                                                                                               0.0s
 => => naming to docker.io/library/zadanie1_alpine:v1                                                                                                                                                                                                                                                      0.0s

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
  
PS D:\sem6\Docker\zad1> docker run -d -p 5001:5000 --name zadanie1_alpine_v1 zadanie1_alpine:v1
6175363d5f985031f0ee60f761593ccd4b22f4357660225e761fc7b850b5cb66
PS D:\sem6\Docker\zad1> 
```
