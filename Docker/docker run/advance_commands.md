# Advanced Commands

```bash
docker run ubuntu:17.10 cat /etc/*release*
```

```bash
docker run -d -e MYSQL_ROOT_PASSWORD=admin mysql
```


```bash
docker run -d --name my-registry -p 5000:5000 registry:2
```

If you miss something later, update it
```bash
docker update --restart always my-registry 
```