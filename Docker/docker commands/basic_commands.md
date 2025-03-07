# Basic Commands

## Containers
Run - Start a Container
```bash
docker run nginx
```

List Containers
```bash
docker ps
docker ps -a
```

Stop a Container
```bash
docker stop <container_ID>
docker stop <container_name>
```

Remove a Container
```bash
docker rm <container_name>
docker rm <container_ID>
```

## Images
List Images
```bash
docker images
```

Remove a images (Delete all dependent containers to remove a image)
```bash
docker rmi <image_ID>
docker rmi <image_name>
```

Pull image
```bash
docker pull nginx
```

Append a command
```bash
docker run ubuntu
docker run ubuntu sleep 5
```

Exec - Execute a command
```bash
docker exec <container_ID> cat /etc/hosts
```

Run - attach or detach
```bash
docker run <image_ID>
docker run -d <image_ID>

docker attach <container_ID>
docker attach <container_Name>
```

