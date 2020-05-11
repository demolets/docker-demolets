# Making Run Commands Permanent

## Alias

```
alias dockervim="        \
  docker run             \
    --rm                 \
    -ti                  \
    -v "'${PWD}'":/data  \
    -w=/data             \
    -u $(id -u):$(id -g) \
    busybox              \
    vi                   \
"
```
|example|notes|
|-------|-----|
| `dockervim foo.txt`       | creates `foo.txt` in current directory and saves here
| `dockervim /data/foo.txt` | same as above, but remember `/data` is the container path
| `dockervim /tmp/foo.txt`  | will not save to host and be destroyed as soon as container is destroyed


|item|description|
|----|-----------| 
| `alias dockervim=" \` | start with dbl-quotes.  This is much easier to use envs
| `-v "'${PWD}'":/data` | need ${PWD} in single quotes so it evaluates every time command is run
| `vi`                  | runs `vi ` and saves relative to current directory.  absolute paths on 


