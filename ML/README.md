# ML
This directory is about machine learning.

## Tools
- [Install Tensorflow](https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/get_started/os_setup.html)

도커로 설치해서 컨테이너 띄워서 실행하는 방법을 추천한다. 도커 이미지 내에 jupyter가 이미 설치되어 있어서 편리하게 시작할 수 있음.
```sh
docker pull tensorflow/tensorflow
docker run -it -p 8888:8888 gcr.io/tensorflow/tensorflow
 ```
