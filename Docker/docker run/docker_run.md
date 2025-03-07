# Docker RUN

RUN - tag:
```bash
docker run <image>:<tag>
```

RUN - STDIN
```bash
docker run -it <image_ID>
```
i = interactive mode

t = terminal


RUN - PORT Mapping
```bash
docker run -p <External_PORT>:<Container_PORT> <image_ID>

docker run -p 80:8080 <Image_ID>
```

RUN - Volume Mapping
```bash
docker run -v <External_dir>:<Container_dir> <image_ID>

docker run -v /opt/datadir:/var/lib/mysql mysql
```

Inspect Container
```bash
docker inspect <container_ID>
```

Container Logs
```bash
docker logs <container_ID>

```