2025/10/10 page 70

2025/10/13 plan/real  100/110

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
