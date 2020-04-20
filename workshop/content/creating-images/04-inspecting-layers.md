To inspect the layers of the container image you just created, run:

```execute
docker history greeting
```

The output should be similar to:

```
ID             CREATED          CREATED BY                                      SIZE      COMMENT
2c7f2c2d7c26   30 seconds ago   /bin/sh                                         9.216kB
83aa35aa1c79   4 weeks ago      /bin/sh -c #(nop) CMD ["sh"]                    0B
<missing>      4 weeks ago      /bin/sh -c #(nop) ADD file:450bea8cddb743e...   1.437MB
```

The top layer has captured the changes you made from the interactive shell session of the running container. The other layers were inherited from the `busybox` container image.

Because you constructed the container image from a running container, there is no way to see what individual commands you ran, or what files you copied into the container.

To see the metadata for the container image, you can also run:

```execute
docker inspect greeting
```

This includes details on the layers, but also information about the command run when the container image is run, and details of any environment variables set by the container image.
