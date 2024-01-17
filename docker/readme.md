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

