# Docker Networking

![Docker Networking](../../images/docker-networks1.png)

![Docker Netwroking](../../images/docker-networks2.png)



```bash
docker inspect network
```

```bash
docker network create --driver bridge --subnet 182.18.0.0/24 --gateway 182.18.0.1 wp-mysql-network
```