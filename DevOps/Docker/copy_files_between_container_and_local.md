# 개요
docker container 내의 파일을 로컬로 scp(secure copy) 해야 한다!
<br/>

# 방법
## [Docker cp](https://docs.docker.com/engine/reference/commandline/cp/)
Copy files/folders between a container and the local filesystem.

1. docker host 접속
2. [docker cp](https://docs.docker.com/engine/reference/commandline/cp/)로 container 내의 디렉토리 copy
```bash
# docker cp ${container_id}:${directory} ${destination_directory}
docker cp 645441627a0a:/app ../
```
3. scp from local to remote(the host)
```bash
scp -r {username}@{host}:{source path} {destination path}
```
