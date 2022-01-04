# Docker Cheatsheet
## Container Management
### Create a container
```bash
docker create image [command]
docker run image [command]
```
### Inspecting the container
List running containers
```bash
docker ps
```
List all containers
```bash
docker ps -a
```
Show low level container info in json
```bash
docker inspect <container>
```
### Interacting with the container
Attach to a running container (stdin/stdout/stderr)
```bash
docker attach container
```
Copy files from and to the contauber
```bash
docker cp container:path hostpath|-
docker cp hostpath|- container:path 
```
## Image management
List all local images
```bash
docker images
```
Show low level image info in json 
```bash
docker inpect <image>
```
Tag an image
```bash
docker tag 
```

# Docker Compose
