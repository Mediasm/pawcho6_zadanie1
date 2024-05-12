Commands:
docker build -t zadanie1_alpine:v1 .
docker run -d -p 5001:5000 --name zadanie1_alpine_v1 zadanie1_alpine:v1

Terminal:
PS D:\sem6\Docker\zad1> docker build -t zadanie1_alpine:v1 .
[+] Building 1.1s (13/13) FINISHED                                                                                                                                                                                                                                                               docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                                                                                                                       0.0s
 => => transferring dockerfile: 688B                                                                                                                                                                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/node:alpine                                                                                                                                                                                                                                             1.0s
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
 => => writing image sha256:3ac06c83dc12663edd17954e2541203e3bd31bdb8ef7a4a471d55b178066792b                                                                                                                                                                                                               0.0s 
 => => naming to docker.io/library/zadanie1_alpine:v1                                                                                                                                                                                                                                                      0.0s 

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview

PS D:\sem6\Docker\zad1> docker run -d -p 5001:5000 --name zadanie1_alpine_v1 zadanie1_alpine:v1
8309138f8f8f05eb14dbde11ec770254ea3632583d007a1d0f2b218155ac95f8
PS D:\sem6\Docker\zad1> 

