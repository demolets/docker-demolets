# docker run

Various ways to run applications in docker without having ot install

## Run a simple non-interactive command

```
docker run \
  --rm    \
   hello-world
```

| | |
|-|-| 
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

| | |
|-|-| 
| `-t` | pseudo-tty for shell like output.  Most commonly paired with:
| `-i` | interactive shell.  necessary for running commands that accept input 