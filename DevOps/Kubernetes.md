# [Kubernetes](https://kubernetes.io/ko/)
컨테이너화된 어플리케이션을 자동으로 배포, 스케일링 및 관리해주는 오픈소스 시스템

## Architecture
![kube architecture](https://1.bp.blogspot.com/-VMBcuIeUCx0/W26-OBALRvI/AAAAAAAABho/ayhh3n6DgHYl_SY9CLece-B-JQs1fTq3QCLcBGAs/s640/kubernetes%2Barchitecture%2Bexplained.jpg)

## 특징
- Go로 작성됨
- Customizable since opensource
- Pod networking

## [Pod](https://kubernetes.io/ko/docs/concepts/workloads/pods/pod-overview/)
- 쿠버네티스 객체 모델 중 만들고 배포할 수 있는 가장 작고 간단한 단위이다(배포의 단위).
- 클러스터에서의 running process를 나타낸다.
- 저장소 리소스, 특정 네트워크 IP, 컨테이너가 동작하기 위해 만들어진 옵션을 캡슐화한다.
- 다중 컨테이너를 관리할 수 있다.
- 같은 파드 안에 속한 컨테이너에게 두 가지 공유 리소스를 제공한다.
  - **네트워킹**: 각각의 파드는 유일한 IP 주소를 할당 받는다.
  - **저장소**: 파드 내부의 모든 컨테이너는 공유 볼륨에 접근할 수 있고, 컨테이너 간 데이터 공유가 가능하다.

## Ingress
쿠버네티스에서 HTTP(S) 기반의 L7 로드밸런싱 기능을 제공하는 컴포넌트이다.
트래픽이 높으면 ingress 갯수를 늘리면 된다.
SSL 인증서도 붙일 수 있다.

![Ingress](https://t1.daumcdn.net/cfile/tistory/99EF73395B2D16940A)

## Useful commands & tools
- [kubectl CLI](https://kubernetes.io/docs/reference/kubectl/overview/): 한 개의 pod의 로그를 볼 수 있음
- [stern CLI](https://github.com/wercker/stern) : 멀티 pod의 로그를 한 번에 볼 수 있음

## 참고
- https://bcho.tistory.com/1263
- http://tech.kakao.com/2018/12/24/kubernetes-deploy/
- https://github.com.ramitsurana/awesome-kubernetes

## Q&A
- ingress에서 ingress로 routing 구성이 가능한가?
  > 한 클러스터 내에서 ingress controller를 내부망/외부망으로 분리 가능
