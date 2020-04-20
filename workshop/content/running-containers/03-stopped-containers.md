When containers are shutdown, the application processes are gone, but a copy of the state of the container state is kept. You can see a list of all containers, including the stopped containers by running:

```execute
docker ps -a
```

Because we have started a number of containers, you should see multiple stopped containers listed.

```
CONTAINER ID  IMAGE                             COMMAND  CREATED             STATUS                     PORT
S  NAMES
45e9a2513d64  docker.io/library/busybox:latest  sh       About a minute ago  Exited (0) 24 seconds ago
   elastic_margulis
16a584405878  docker.io/library/busybox:latest  date     2 minutes ago       Exited (0) 2 minutes ago
   adoring_mendeleev
10643c0c755e  docker.io/library/busybox:latest  date     3 minutes ago       Exited (0) 3 minutes ago
   practical_elbakyan
```

When we ran the containers, we ran them in the foreground, with any output from the containers displayed in the terminal.

The output from the container was also captured to a log file. You can view the log file for a container, running or stopped, by running the `docker logs` command with the container ID as argument.

```execute
docker logs `docker ps -ql`
```

In addition to the log file for a container, a copy of changes made to the filesystem from within the container are also kept. It is possible to copy files out of the stopped container, or create a new container image from a stopped container.

Although there are some uses for a stopped container, they do consume space, so it is important to delete the stopped containers. If you do not do so, eventually you will run out of disk space.

To delete a single stopped container, you can use `docker rm` with the container ID as argument.

```execute
docker rm `docker ps -ql`
```

You should now have just the two stopped containers remaining.

```execute
docker ps -a
```

To delete all stopped containers, run:

```execute
docker rm $(docker ps -aq)
```

Although `docker ps -a` will respond with running containers as well as stopped containers, the `docker rm` command will only delete stopped containers.

There should now be no remaining containers.

```execute
docker ps -a
```

If you know that you do not need to interact with the stopped container after it has been shutdown, you can use the `--rm` option when running `docker run`.

```execute
docker run --rm busybox date
```

With this option, the stopped container will be automatically deleted.

```execute
docker ps -a
```
