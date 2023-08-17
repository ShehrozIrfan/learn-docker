## Run a Container

- Asks Docker to create and run a container based on the hello-world image:
  
  ```
  docker run hello-world
  ```

## Container Management Commands

- Get help for Docker commands from the command line itself using the –help switch:

  ```
  docker run --help
  ```

- Lists the containers that are still running:

  ```
  docker ps
  ```

- Add the -a switch in order to see containers that have stopped:

  ```
  docker ps -a
  ```

- Retrieves the logs of a container, even when it has stopped:

  ```
  docker logs <container_id>
  ```

- Gets detailed information about a running or stopped container:

  ```
  docker inspect <container_id>
  ```

- Stops a container that is still running:

  ```
  docker stop <container_id>
  ```

- Deletes a container:

  ```
  docker rm <container_id>
  ```

- Running one docker rm command for each stopped container. The -f switch is an implicit confirmation to proceed and delete all stopped containers right away,
  instead of asking to confirm that operation:

  ```
  docker container prune -f
  ```

## Running a Server Container

- Run the container in the background, and use the detach switch `-d`:

  ```
  docker run -d alpine ping www.docker.com
  ```
  Note the addition of a `-d` switch. When doing so, the container starts, but we don’t see its output. Instead, the docker run command returns the ID of the
  container that was just created.

- In the `docker logs` get a portion of the output using the –from, –until, or –tail switches. Let’s see the most recent 10 seconds of logs for our running container:

  ```
  docker logs --since 10s <container_id>
  ```

- Listening for Incoming Network Connections:
  Use the `-p` switch on the `docker run`. The -p switch takes two parameters; the incoming port you want to open on the host machine, and the port to which it
  should be mapped inside the container. For instance, here is how I state that I want my machine to listen for incoming connections on port 8085 and route
  them to port 80 inside a container that runs NGINX:

  ```
  docker run -d -p 8085:80 nginx
  ```

## Using volumes

Any data stored in that database will be lost when the container is stopped or restarted. In order to avoid data loss, you can use a volume mount:

```
docker run -v /your/dir:/var/lib/mysql -d mysql:5.7
```
It will ensure that any data written to the `/var/lib/mysql` directory inside the container is actually written to the `/your/dir` directory on the host system. 
This ensures that the data is not lost when the container is restarted.

--- ---

- Although the docker run command downloads images automatically when missing, you may want to trigger the download manually.
  To do this, you can use the `docker pull` command. A pull command forces an image to download, whether it is already present or not.

- List the docker images:

  ```
  docker image ls
  ```
