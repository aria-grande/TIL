# ML
This directory is about machine learning.

## TO READ
- https://www.kaggle.com/joparga3/2-tuning-parameters-for-logistic-regression

## Tools
### [Install Tensorflow](https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/get_started/os_setup.html)

도커로 설치해서 컨테이너 띄워서 실행하는 방법을 추천한다. 도커 이미지 내에 jupyter가 이미 설치되어 있어서 편리하게 시작할 수 있음.
```sh
docker pull tensorflow/tensorflow
docker run -it -p 8888:8888 tensorflow/tensorflow
 ```

### Jupyter
- 수식 변환기: http://jupyter-notebook.readthedocs.io/en/latest/examples/Notebook/Typesetting%20Equations.html

### 종합셋트 docker image
https://github.com/okwrtdsh/anaconda3

Anaconda3, Jupyter Notebook, OpenCV3, TensorFlow and Keras2 넘파이와 scipy도 물론 있다!
