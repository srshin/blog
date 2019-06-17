## Docker
* docker hub : https://hub.docker.com/
### 기본 명령
```
docker --version
docker version
```
* 리스트
```
$ docker images
$ docker container ps -a
$ docker commit my-ubuntu my_ubuntu_vim  #.컨테이너를 이미지로 생성
```
* 지우기 (컨테이너 멈춤- 지우기 - 이미지지우기)
```
$ docker container stop 숫자앞부분
$ docker container rm -f 컨테이너 삭제
$ docker container rm $(docker container ls -a -q)
$ docker image rm $(docker image ls -a -q)
$ docker rmi [imageid]
```

### docker-machine
```
docker-machine ssh
docker-machine restart
docker-machine stop
```
### docker build
```
docker build -t [tag]  
* ex : docker build -t my_docker_img
```
### docker-compose 
```
$ docker-compose build
$ docker-compose up
$ docker-compose down -v
$ docker-compose stop
$ docker-compose ps
```
* run
```docker-compose run [service_name] [command]
* ex : docker-compose run app bash
* ex : docker-compose run app python manage.py migrate
```
### docker container
* run 
```docker run -dit -v [folder]:[folder] [image_name]
* ex : docker run -dit -v /d/program/git:/src ubuntu
* ex : docker run -it --rm -v "/d/program/git/python":/tf/notebooks -p 8888:8888 tensorflow/tensorflow:latest-py3-jupyter
* ex : docker run -dit   -v /d/program/git/python:/src ubuntu
```
* exec
```docker exec -it [container_name] [command]
$ docker exec -it my-ubuntu echo 'hello world'
* ex : docker exec -it ubuntu2 bash
```
### nginx
```
$ docker pull nginx
$ docker container run --name webserver -d -p 80:80 nginx
virtualbox proxy forwarding 80 -> 80으로 추가후 웹접속 localhost 
$ docker stop webserver
```
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

