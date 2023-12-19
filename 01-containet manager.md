# Container management commands
command description


docker create image [ command ] create the container
docker run image [ command ] = create + start
docker rename container new name rename the container
docker update container update the container config
docker start container. . . start the container
docker stop container. . . graceful2 stop
docker kill container. . . kill (SIGKILL) the container
docker restart container. . . = stop + start
docker pause container. . . suspend the container
docker unpause container. . . resume the container
docker rm [ -f3
] container. . . destroy the container
2
send SIGTERM to the main process + SIGKILL 10 seconds later
3
-f allows removing running containers (= docker kill + docker rm)
