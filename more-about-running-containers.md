## Restart Mode:
When creating a container, you have the choice to set a restart mode. It tells Docker what to do when a container stops. 
A restart mode is set with the `--restart` switch:

```
docker run -d -p 80 --restart always nginx
```

It works great. Should the container start, or the Docker host itself restart, the container will restart so that it has a high uptime. 
But it actually works too well; if you try to stop the container using the docker stop command, it will not stop.

That’s probably not what you want. If you want your container to always be running except when you explicitly stop it, use the unless_stopped restart mode:

```
docker run -d -p 80 --restart unless-stopped nginx
```

## Monitoring:

```
docker stats
```
This will output a live list of running containers plus information about how many resources they consume on the host machine. 
Like a docker ps extended with live resource usage data.

## Reclaim Disk:
Here are the commands you can run to remove the items that you don’t need:

```
docker container prune -f
docker volume prune -f
docker image prune -f
```

If you want to remove all unused images, just use the following command:

```
docker image prune --all
```
