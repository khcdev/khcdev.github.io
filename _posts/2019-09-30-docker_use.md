---
title:  "Docker 활용(1) - 이미지 빌드 및 컨테이너 관리"
search: false
categories: 
  - docker
last_modified_at: 2018-09-29T19:00:00+09:00
---


# Docker 컨테이너 실행, 이미지 빌드... etc

## Docker 명령
  `docker run`, `docker rmi` 등과 같이 `docker <명령>`의 형태 이다.
  docker 명령은 항상 관리자 권한으로 실행 되어야함.

Tip!
  ```bash
  $ sudo usermod -aG docker ${USER}
  $ sudo service docker restart
  혹은 상단 고래모양 아이콘 클릭하고 restart
  ```
## [Dockerhub]((https://hub.docker.com/)) 
  github같은 공용 docker image repository

  nginx, redis, python, django등 다양한 어플리케이션들의 공식 이미지등이 업로드 되어 있으며 개인이 빌드한 이미지도 업로드 하여 공유할 수 있는 공개적인 레파지토리이다. 

  공식 이미지를 사용하고 싶은 경우  `OFFICIAL IMAGE` 마크를 꼭 확인 할 것 

  보통 공식 이미지들은 해당 이미지를 어떻게 사용할지 간단한 가이드를 제공 하고 있다.  [dockerhub nginx 페이지](https://hub.docker.com/_/nginx)
   
  ### 실습
  nginx 이미지 pull 받아 로컬에 띄워보고 해당 컨테이너에 접속해볼 것
  
  1. ##### 이미지 pull 
  
  `docker pull nginx`
    
  image 확인 `docker images`
  
  2. ##### 컨테이너 실행 
  
  `docker run --name <컨테이너 이름> -d -p 5000:80 <image 이름:태그 | image_id>` 
      
      > 도커 컨테이너 실행에서 기본이 되는 명령어 간단 설명

      `run` : docker container를 실행시킴 </br>
      `--name` : 실행되는 컨테이너에 네이밍, 이미지 이름을 지정하지 않으면 랜덤 명명</br>
      `-d` : detach mode 이 옵션을 주지 않으면 </br>
      `-p` : container의 포트 master host에 publish </br>

  추가적인 옵션 상세한 설명은  `docker run --help`

  3. ##### 실행중인 컨테이너 확인 

  ``` shell
  docker ps
  ```
  
  `docker container ls (-a)`

  4. ##### 실행중인 컨테이너에 command 실행
  `docker exec [options] <container> <command> [arg...]`
  
  ex) 컨테이너 접속
  `docker exec -it <이미지이름:tag | image_id> <command>`

  컨테이너가 실행된 시점으로 진입`docker attach`
  
  5. ##### container 변경사항 확인 및 commit
  
   컨테이너 변경사항 확인

  `docker diff <container>`

   컨테이너 변경사항 커밋

  `docker commit <container> <docker_image>`

# Dockerfile 통해 Image 빌드
### Dockerfile?
Dockerfile 이미지 설정 파일, docker image 빌드시 Dockerfile에 작성한 대로 docker image가 생성 된다.


  ### 실습
  1. nginx docker image 기반으로 새로운 html페이지 만들어 빌드 및 실행
  
  2. nginx container에 외부 디렉토리 연결하여 새로운 html 파일 공유

### Publisher Dockerfile
```dockerfile
FROM python:3.6.5   # python:3.6.5 이미지 베이스로 함

ENV PYTHONUNBUFFERED 1 # 환경변수 set

RUN apt-get -y update && apt-get install -y gifsicle
COPY requirements.txt /usr/src/Publisher/
WORKDIR /usr/src/Publisher
RUN pip install --no-cache-dir -r requirements.txt

COPY . /usr/src/Publisher
EXPOSE 8000
...
```

##### RUN 

- 도커이미지가 생성되기 전에 수행할 쉘 명령어

### ENV
- 환경변수 값 설정

##### WORKDIR  

- CMD에서 설정한 실행 파일이 실행될 디렉토리

##### ADD
- 파일 혹은 디렉토리를 docker image내의 지정한 위치로 copy한다.

- 만일 ADD 할려고 하는 파일이 tar 압축파일 이면 docker가 자동으로 압축을 풀어서 ADD 한다. 

- Directory를 ADD하기 위해서는 /로 끝나야 한다. 주의할점은 빌드 directory 외부의 파일은 ADD 할 수 없다.

- ADD 할려고 하는 파일이나 디렉토리와 같은 이름의 파일이나 디렉토리가 벌써 image 상에 존재 한다면 덮어 씌우지 않는다.


##### COPY 
- ADD와 기본적으로 동일하나 차이점은 URL을 지정할수 없고 압축파일을 자동으로 풀어주지 않는다.

- COPY도 ADD와 마찬가지로 빌드 디렉토리 밖의 파일들은 COPY 할 수 없다. 그 이유는, COPY (혹은 ADD) 가 호스트에서 이루어지는것이 아니라 현재 빌드 디렉토리 자체가 Docker daemon에 upload 된 후 거기서 이루어지기 때문이다.


##### VOLUME 

- VOLUME은 디렉터리의 내용을 컨테이너에 저장하지 않고 호스트에 저장하도록 설정

- 데이터 볼륨을 호스트의 특정 디렉터리와 연결하려면 docker run 명령에서 -v 옵션을 사용해야 한다.

  ex) -v /root/data:/data

- 주로 로그수집이나 데이터 수집할 때 필요

##### CMD

- 컨테이너가 시작되었을 때 실행할 실행 파일 또는 셸 스크립트

##### ENTRYPOINT
- CMD와 비슷하지만 차이점은 override 될 수 없다.
- DockerFile내 1회만 사용 가능


##### EXPOSE 
- 호스트와 연결할 포트 번호

### .dockerignore
.gitignore와 같은 역할을 한다. docker image 빌드시에 이미지에 포함되지 않아도 되는 파일들을 제외할 수 있다.


# 이미지 푸쉬
`docker push <image:tag>`

### 연동개발팀 프로젝트 살펴보기 

