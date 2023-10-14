## SSH Into A Docker Container

Get the name of the existing container:

```bash
$ docker ps
```

to list the currently running containers and find the name of the one you want to connect to. If you don't see the one you are looking for, it may not be
running.

Use the command `docker exec -it <container name> /bin/bash`
to get a bash shell in the container


Generically, use `docker exec -it <container name> <command>`
to execute whatever command you specify in the container.

[source](https://phase2.github.io/devtools/common-tasks/ssh-into-a-container/#how-do-i-run-a-command-in-my-container)