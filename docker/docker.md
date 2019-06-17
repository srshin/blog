## Docker
* docker hub : https://hub.docker.com/

### mysql 
* quick run 
```
$ docker pull mysql:5.7
$ docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 mysql:5.7
C:\Users\home>mysql -h192.168.99.100 -p1234 -uroot
```
* container 이름
```
$ docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 --name mysql5 mysql:5.7
$ docker exec -it mysql5 bash
root@c9f277173f3c:/# cat /etc/issue
root@c9f277173f3c:/# which mysql
root@c9f277173f3c:/# mysql --user root --password
```
* volum mount 
```
$ docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 -v /d/program/git/docker/mysql:/var/lib/mysql mysql:5.7 --innodb_use_native_aio=0
```

