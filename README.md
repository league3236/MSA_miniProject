# MSA_miniProject
MSA mini Project using Kubernetes

## Info
- 목적 : Docker Build & Kubernetes Build
- 구성요소 : Nginx/HtmlCode
- 요건 : Docker Build와 Kubernetes 배포 Script

## Folder Architecture
* DockerScript : ./docker
* KubernetesScript : ./kubernetes

## Pre requisites (Docker QuickStart Deamon에서 실행)
```
$ cd ~/MSA_miniProject
$ mdir docker
$ mkdir kubernetes
$ touch docker/build.sh
$ touch docker/push.sh
$ touch kubernetes/kubProvisioning.sh
$ git config --global user.name "mincloud1501"
$ git config --global user.email "mincloud1501@naver.com"
$ cat .git/config
```

## Usage
* Git Push
```
$ git add -A
$ git commit -m "first"	// Local Repository
$ git push // Remote Repository
```

* Docker File Edit [/docker/build.sh]
```
docker build --rm -t mincloud1501/nginx .
docker run -d --rm --name nginx1 -p 8888:80 mincloud1501/nginx
```
* Docker Build
```
cd ./docker
. build.sh
```
* Docker Check
```
$ docker images
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
mincloud1501/nginx   latest              40f4b6da1e0f        24 seconds ago      109MB

$ docker ps -a
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS              PORTS                  NAMES
b9c7b72516dc        mincloud1501/nginx   "nginx -g 'daemon of…"   7 seconds ago       Up 7 seconds        0.0.0.0:8888->80/tcp   nginx1

$ docker-machine ip
192.168.99.100
```
[Test Page Connection]
* http://docker-machine ip:8888/

* Docker Hub Push
```
. push.sh
```

* Kubernetes Provisioning
- Pre requisites
  * MSA_miniProject Directory를 C:\Users\GKN\kubernetes-vagrant-centos-cluster 아래로 이동

[kubernetes Node1] 에서 실행
```
[root@node1 ~]# kubectl delete deploy/nginx1; kubectl run nginx1 --image=mincloud1501/nginx --port=80 -o yaml > deploy.yaml

[root@node1 ~]# kubectl create -f deploy.yaml 로 확인
```

[생성한 deploy yaml 파일내용을 kubProvisioning.sh로 편집 후 실행]
```
cd ./Kubernetes
. kubProvisioning.sh
```

* Kubernetes Git Hub Push
```
git push
```