
`$ sudo docker pull ubuntu`
`$ sudo docker run -ti ubuntu /bin/bash`

`$ apt update`
`$ apt install lsb-core`
`$ apt install clang`
`$ clang --version`
`Ubuntu clang version 14.0.0-1ubuntu1`

`$ docker ps`
:

```
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
3d28022df2a3   ubuntu    "/bin/bash"   3 minutes ago   Up 3 minutes             adoring_roentgen
```

`$ docker commit -p ubuntu lang2`
- `Error response from daemon: No such container: ubuntu`
- image nameではなくcontainer idを使う
`$ docker commit -p 3d28022df2a3 lang2`

`$ sudo docker run -ti -v ~/langbook2/sample_codes:/data ubuntu /bin/bash`
