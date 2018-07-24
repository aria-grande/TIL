# Docker container 내 파일 전송
## running container의 파일 -> local
1. docker host 접속
2. [docker cp](https://docs.docker.com/engine/reference/commandline/cp/)로 container 내의 디렉토리 copy
```bash
# docker cp ${container_id}:${directory} ${destination_directory}
docker cp 645441627a0a:/app ../
```
3. scp from local to remote(the host)
```bash
scp -r deploy@test.aria.com:~/app/test.csv .
```
