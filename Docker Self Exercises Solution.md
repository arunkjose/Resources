## Self Exercises – Solutions

### Part 1: Basic Docker Commands

**Task 1:**
```bash
docker pull alpine
docker container run -it --name myalpine alpine
touch hello.txt
ls
exit
docker ps -a
```

**Task 2:**
```bash
docker container run -it --name deb01 debian
apt update && apt install curl -y
curl https://example.com
exit
docker container attach deb01
Ctrl+P+Q to detach
docker exec deb01 ls /
```

**Task 3:**
```bash
docker container run -d --name myweb httpd
docker ps
docker exec -it myweb /bin/bash
ls /usr/local/apache2/htdocs
exit
docker container stop myweb
docker container rm myweb
docker image rm httpd
```

---

### Part 2: Docker Lifecycle

**Task 4:**
```bash
docker pull mysql:5.7
docker container create --name dbtest -e MYSQL_ROOT_PASSWORD=admin123 mysql:5.7
docker container start dbtest
docker container pause dbtest
docker container unpause dbtest
docker logs dbtest
docker stats dbtest
docker container stop dbtest
docker container rm dbtest
```

**Task 5:**
```bash
docker container ls -a
docker image ls
docker container prune -f
docker image prune -a -f
docker system df
```

---
