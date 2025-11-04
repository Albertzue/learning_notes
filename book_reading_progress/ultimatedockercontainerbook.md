2025/10/10 page 70

2025/10/13 plan/real  100/110

2025/10/19  121

2025/10/20  160/166

2025/11/04  256/288
## Keypoints:

**Moby project**
<img width="1508" height="829" alt="image" src="https://github.com/user-attachments/assets/1d2a4308-756d-4f96-a5b0-b5c6cfb60e80" />

**Container architecture**
<img width="741" height="508" alt="image" src="https://github.com/user-attachments/assets/72c5c51f-8aff-4b54-9aa4-9a43178f382e" />

**runc** is the low-level functionality of the container runtime such as
container creation or management, while **containerd**, which is based on runc, provides higher-level
functionality such as image management, networking capabilities, or extensibility via plugins. B


```
docker container inspect -f "{{json .State}}" trivia | jq .
```

```
docker container exec -i -t trivia /bin/sh
```
The -i (or --interactive) flag signifies that we want to run the additional process interactively, \
and -t (or --tty) tells Docker that we want it to provide us with a TTY (a terminal emulator) for \
the command. Finally, the process we run inside the container is /bin/sh.

```
 docker container attach trivia2
```
We can use the attach command to attach our terminal’s standard input, output, or error (or any
combination of the three) to a running container using the ID or name of the container. 

<img width="699" height="331" alt="image" src="https://github.com/user-attachments/assets/e2bd0266-3288-4667-81d1-c0acd80e4a2a" />


#### The COPY and ADD keywords

The COPY and ADD keywords are very important since, in the end, we want to add some content to
an existing base image to make it a custom image. Most of the time, these are a few source files of –
say – a web application, or a few binaries of a compiled application.

These two keywords are used to copy files and folders from the host into the image that we’re building.
The two keywords are very similar, with the exception that the ADD keyword also lets us copy and
unpack TAR files, as well as provide an URI as a source for the files and folders to copy.

Let’s look at a few examples of how these two keywords can be used, as follows:
```
COPY . /app
COPY ./web /app/web
COPY sample.txt /data/my-sample.txt
ADD sample.tar /app/bin/
ADD http://example.com/sample.txt /data/
```

```
ADD --chown=11:22 ./data/web* /app/data/
```
The preceding statement will copy all files starting with web and put them into the /app/data folder in the image, and at the same time assign user 11 and group 22 to these files.

---
```
RUN cd /app/bin
RUN touch sample.txt
```
```
WORKDIR /app/bin
RUN touch sample.txt
```
The former will create the file in the root of the image filesystem, while the latter will create the file at the expected location in the /app/bin folder. Only the WORKDIR keyword sets the context across
the layers of the image. The cd command alone is not persisted across layers.

---
Now that we have dealt with this, we can get back to CMD and ENTRYPOINT. ENTRYPOINT is used to define the command of the expression, while CMD is used to define the parameters for the
command. Thus, a Dockerfile using Alpine as the base image and defining ping as the process to run in the container could look like this:
```
FROM alpine:3.17
ENTRYPOINT [ "ping" ]
CMD [ "-c", "3", "8.8.8.8" ]
```
The beauty of this is that I can now override the CMD part that I have defined in the Dockerfile(remember, it was ["-c", "3","8.8.8.8"]) when I create a new container by adding the new values at the end of the docker container run expression, like this:
```
$ docker container run --rm -it pinger -w 5 127.0.0.1
```

If we want to override what’s defined in ENTRYPOINT in the Dockerfile, we need to use the --entrypoint parameter in the docker container run expression. Let’s say we want to execute a shell in the container instead of the ping command. We could do so by using the following command:
```
$ docker container run --rm -it --entrypoint /bin/sh pinger
```
```
FROM alpine:3.17
CMD wget -O - http://www.google.com
```
Here, I have even used the shell form to define CMD. But what happens in this situation if ENTRYPOINT is undefined? If you leave ENTRYPOINT undefined, then it will have the default value of /bin/sh -c, and whatever the value of CMD is will be passed as a string to the shell command. The preceding definition would thereby result in entering the following code to run the process inside the container:
```
/bin/sh -c "wget -O - http://www.google.com"
```
---
```
docker container run -it --name reader \
    -v shared-data:/app/data:ro \
    ubuntu:22.04 /bin/bash
```
Here we have a container called reader that has the same volume mounted as read-only (ro).

---

```
ARG BASE_IMAGE_VERSION=12.7-stretch
FROM node:${BASE_IMAGE_VERSION}
WORKDIR /app
COPY packages.json .
RUN npm install
COPY . .
CMD npm start
```
if we want to create a special image for, say, testing purposes, we can override this variable at
image build time using the --build-arg parameter, as follows:
```
docker image build \
    --build-arg BASE_IMAGE_VERSION=12.7-alpine \
    -t my-node-app-test .
```

```
  docker image build  -f Dockerfile.dev -t node-demo-dev .
```
Please note the -f Dockerfile.dev command-line parameter. We must use this since we are using a Dockerfile with a non-standard name.

#### delete dangling images:
```
docker image prune -f
```

When Docker builds an image, it first sends all of the files in the current directory (known as the “build context”) to the Docker daemon. If this directory contains large files or directories that aren’t necessary for building the Docker image (such as log files, local environment variables, cache files, etc.), these can be ignored to speed up the build process.


Here’s an example of a .dockerignore file:
```
# Ignore everything
**
 # Allow specific directories
 !my-app/
 !scripts/
 # Ignore specific files within allowed directories
 my-app/*.log
 scripts/temp/
```
