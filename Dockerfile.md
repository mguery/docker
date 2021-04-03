Copied from [@adamveld](https://gist.github.com/adamveld12/4815792fadf119ef41bd#file-dockerfile-md)

Set the base image to Ubuntu *must be first instruction* - use docker search to find images

```dockerfile
FROM ubuntu # <image>
FROM ubuntu:latest # - <image>:<tag>
FROM ubuntu:precise (LTS)
```

Set the maintainer info
```dockerfile
MAINTAINER Adam Veldhousen, adam@veldhousen.ninja # <name>
```

Copy a local/remote file into the container 
Also supports auto extracting of .tar.gz into destination and can copy from remote locations (ie raw.github)
```dockerfile
ADD ./index.html /var/www/index.html # <src> <dest>
```

Prefer copy over add: http://docs.docker.com/articles/dockerfile_best-practices/#add-or-copy
Copy only supports copying local files
```dockerfile
COPY ./index.html /var/www/index.html
```

Sets the user name to use 
```dockerfile
USER username
```
ENV set env vars
```dockerfile
ENV KEY 1234 # <key> <value>
```

Runs a command on the image and commits the result
```dockerfile
RUN apt-get install vim # <command> - equivalent to docker run ubuntu apt-get install vim && docker commit XXXX
```

The WORKDIR directive is used to set where the command defined with CMD is to be executed.
```
WORKDIR /home/dev
```

Like an exec, preferred (A minimal $PATH only)
```dockerfile
ENTRYPOINT ["executable", "param1", "param2"] 
```

Execute as a shell (Your $PATH is setup this way)
```dockerfile
ENTRYPOINT command param1 param2 
```

this:
```dockerfile
CMD ["-l","-"]
ENTRYPOINT ["/usr/bin/wc"]
```


and this:
```dockerfile
ENTRYPOINT wc -l -
```

and this:
```dockerfile
ENTRYPOINT ["wc", "-l", "-"]
```

are all equivalent

Exposes this port on the container to the outside world
```dockerfile
EXPOSE 80 # <port> [<port>...]
```

Adds one or more new volumes to any container created from the image
```dockerfile
VOLUME ["/data"] # [<volumes>...], puts /data -> /var/lib/docker/volumes/
```
