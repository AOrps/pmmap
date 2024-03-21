# Docker 

## Common Errors
```txt
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/images/json": dial unix /var/run/docker.sock: connect: permission denied
```

- To rectify, do the following commands:
```bash
sudo usermod -aG docker $USER

sudo systemctl restart docker

sudo systemctl enable docker
```

- **Note**: Sometimes docker still doesn't want to play nice so a `sudo reboot now` or computer restart should do the trick! 


## Install
- Pacman
```sh
pacman -S docker docker-buildx
```

- Debian
```
apt install docker
```


## General
- Docker uses a layered architecture.
```Dockerfile
# ----------- v1
FROM debian

RUN apt install x y z 

RUN pip install px py pz

COPY . /opt/src-code

ENTRYPOINT APP=/opt/src-code/run

# ----------- v2
FROM debian

RUN apt install x y z 

RUN pip install px py pz

COPY . /opt/diff-src-code

ENTRYPOINT APP=/opt/diff-src-code/run
```
- Docker will cache the same base, and then edit the diff to save time and resources.

- Image Layers: Read Only (when using `docker build`)
- Container Layer: Read / Write (when using `docker run`)

### volumes
- `-v` is the original way, but `--mount` is the preferred method.

- Volumes are located in `/var/lib/docker/volumes`

<!-- ```mermaid -->
<!-- --- -->
<!-- title:  -->
<!-- --- -->

<!-- stateDiagram-v2 -->
<!-- 	subgraph  -->
<!-- ``` -->


- There are 2 types of volumes:
  - Bind Mount   (external ie not volume created by docker)
  - Volume Mount (volumes created by docker via `docker volume create <VOLUME_NAME>`)


- Storage drivers
  - aufs
  - zfs
  - btrfs
  - device mapper
  - overlay
  - overlay2


- Volume Drivers
  - Local
  - Azure File Storage
  - ...


## Docker Filesystem
- Located in `/var/lib/docker`
```tree
/var/lib/docker/
├── buildkit
├── containers      ; all files related to containers
├── image           ; files related to images
├── network
├── overlay2
├── plugins
├── runtimes
├── swarm
├── tmp
└── volumes         ; volumes created by docker
```


