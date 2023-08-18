## Creating a simple image

A Docker image is created using the docker build command and a Dockerfile file. 
The Dockerfile file contains instructions on how the image should be built.

#### Dockerfile:

```
FROM debian:11

CMD ["echo", "Hello world"]
```

In order to create an image from my Dockerfile file, I need to run the docker build command:

```
docker build -t hello .
```

The `-t` switch is used in front of the desired image. 
An image can be created without a name, it would have an auto-generated unique ID, so it is an optional parameter on the docker build command.

Note the dot at the end of the command above. It specifies which path is used as the build context (more about that later), and where the Dockerfile 
is expected to be found. Should my Dockerfile have another name or live elsewhere, I can add a `-f` switch in order to provide the file path.

To run the image:

```
docker run hello
```

## Creating an Image Including Files

#### index.html:

```
<html>
  <body>
    <h1>Hello !</h1>
    <div>I'm hosted by a container.</div>
  </body>
</html>
```

#### Dockerfile:

```
FROM nginx:1.15

COPY index.html /usr/share/nginx/html
```

To build and run:

```
docker build -t webserver .
docker run --rm -it -p 8082:80 webserver
```

The above commands build a webserver from the Dockerfile file instructions, then start a container that listens to my machine’s 8082 port and redirect the 
incoming connections to the container’s 80 port. You can start a browser and point it to http://localhost:8082 to view it locally. This displays the HTML file 
contents in the browser since they are served over HTTP by the running container.

To remove the docker image use:

```
docker rmi <image name or image id>
```

In order to apply a tag, just state it during your build command:

```
docker build -t hello:1.0 .
```

where `1.0` is the image tag.

## Parameters as Environment Variables

[Read here](https://www.educative.io/courses/docker-for-developers/YQqmAQ77D0K)
