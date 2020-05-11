# docker run

Various ways to run applications in docker without having ot install.  Be sure the user is part of the `docker`

## Run a simple non-interactive command

```
docker run \
  --rm    \
   hello-world
```

|item|description|
|----|-----------| 
| `--rm` | remove the container after the run is complete.  This is important for one-off bash-like commands.

## Run an interactive command

```
docker run \
  --rm     \
  -t       \
  -i       \
  busybox  \
  bc
```

|item|description|
|----|-----------| 
| `-t`      | pseudo-tty for shell like output.  Most commonly paired with `-i` as `-ti`
| `-i`      | interactive shell.  necessary for running commands that accept input 
| `busybox` | docker image to run
| `bc`      | command in container to run interactively

## Run interactive command, reading file

```
docker run    \
  --rm        \
  -ti         \
  -v ${PWD}/README.md:/data/README.md \
  -w="/data"  \
  busybox     \
  cat README.md 
```

|item|description|
|----|-----------| 
| `-v ${PWD}/README.md:/data/README.md:ro` | mount existing file. it must exist, otherwise it'll create an empty. directory on the container. `${PWD}` is for current diretory and probably the most portable form (less portable alternatives: $PWD, $(pwd), etc).  Finally, make it read-only with `:ro`.
| `-w="/data"`    | set the working diretory
| `cat README.md` | cats out the file in host's working directory


## Run interactive command, manipulate file in directory

```
docker run             \
  --rm                 \
  -ti                  \
  -v ${PWD}:/data      \
  -w="/data"           \
  -u $(id -u):$(id -g) \
  busybox              \
  vi README.md
```

|item|description|
|----|-----------| 
| `-v ${PWD}:/data` | mount the local directory instead of individual file.  Necessary to create a new file and easier to write
| `-u $(id -u):$(id -g)` | run the container with UID/GID of current user.  Very useful for not leaving root owned files everywhere.

