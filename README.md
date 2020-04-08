<p align="center">
    <img src="https://wiki.multitheftauto.com/images/thumb/5/58/Mtalogo.png/150px-Mtalogo.png">
</p>

What is Multi Theft Auto?
--------------

Multi Theft Auto (MTA) is a multiplayer modification for the Microsoft Windows version of Rockstar North's Grand Theft Auto: San Andreas that adds online multiplayer functionality. For Grand Theft Auto: San Andreas, the mod also serves as a derivative engine to Rockstar's interpretation of RenderWare.

For more information and related downloads for Multi Theft Auto and Server, please visit <https://wiki.multitheftauto.com>.

Supported Tags and Respective Dockerfile Links
----------------------------------------------

-   Multi Theft Auto Server (tag: [`latest`](https://github.com/devzolo/docker-mta-server/blob/master/docker/mta-server/Dockerfile)) ([mta-server/Dockerfile](https://github.com/devzolo/docker-mta-server/blob/master/docker/mta-server/Dockerfile))

How to Use the MTA Server Images
---------------------------

### Downloading a MTA Server Docker Image

Downloading the server image in a separate step is not strictly necessary; however, performing this before you create your Docker container ensures your local image is up to date.

To download the MTA Server image, run this command:

    shell> docker pull devzolo/mta-server:tag
&nbsp;
Refer to the list of supported tags above. If `:tag` is omitted, the `latest` tag is used, and the image for the latest version of MTA Server is downloaded.

### Starting a MTA Server Instance

Start a new Docker container for the MTA Server with this command:


```
# [COMMAND] Options:

* -v                   Shows the program version
* -s                   Run server in silent mode
* -x                   Disable simplified crash reports (To allow core dumps)
* -D [PATH]            Use as base directory
* --config [FILE]      Alternate mtaserver.conf file
* --ip [ADDR]          Set IP address
* --maxplayers [max]   Set maxplayers
* --novoice            Disable voice communication
```
```
    shell> docker run --name=server1 -d devzolo/mta-server:tag [COMMAND...]
```

The `--name` option, for supplying a custom name for your server container (`server1` in the example), is optional; if no container name is supplied, a random one is generated. If the Docker image of the specified name and tag has not been downloaded by an earlier `docker pull` or `docker run` command, the image is now downloaded. After download completes, initialization for the container begins, and the container appears in the list of running containers when you run the `docker ps` command; for example:
```
    shell> docker ps
    CONTAINER ID   IMAGE                COMMAND                  CREATED             STATUS                              PORTS                           NAMES
    a24888f0d6f4   devzolo/mta-server   "./app/mta-server64 .."  14 seconds ago      Up 13 seconds (health: starting)    22003/udp, 22005/tcp 22126/udp  server1
```
The container initialization might take some time. When the server is ready for use, the `STATUS` of the container in the output of the `docker ps` command changes from `(health: starting)` to `(healthy)`.

The `-d` option used in the `docker run` command above makes the container run in the background. Use this command to monitor the output from the container:
```
    shell> docker logs server1
```

---
## Examples

### Starting Default MTA Server Instance
```
    shell> docker run --name=default-mta-server -p 22003:22003/udp -p 22005:22005/tcp -p 22126:22126/udp -d devzolo/mta-server:latest
```
