# Kafka

## 용어 정리
- Broker: 카프카 어플리케이션이 설치되어 있는 서버 또는 노드.
- Topic: 프로듀서와 컨슈머들이 카프카로 보낸 자신들의 메세지를 구분하기 위한 네임. 디비 테이블과 비슷한 개념이라고 생각.
- Partition: 병렬처리가 가능하도록 토픽을 나눌 수 있고, 많은 양의 메세지 처리를 위해 파티션의 수를 늘려줄 수 있다.
- Producer: 메시지를 생산하여 브로커의 토픽 이름으로 보내는 서버 또는 어플리케이션.
- Consumer: 브로커의 토픽 이름으로 저장된 메시지를 가져가는 서버 또는 어플리케이션.

## Producer

### Options
- bootstrap.servers

  카프카 클러스터는 클러스터 마스터라는 개념이 없기 때문에 클러스터 내 모든 서버가 클라이언트의 요청을 받을 수 있다. 이 옵션은 카프카 클러스터에 처음 연결을 하기 위한 호스트와 포트 정보로 구성된 리스트 정보를 나타낸다.
  `hostname1:port1,hostname2:port2`의 포맷으로 구성할 수 있다. 전체 카프카 리스트가 아닌 호스트 하나만 입력해 사용할 수 있지만 이 방법은 추천하지 않는다. 카프카 클러스터는 살아있지만 해당 호스트만 장애가 발생할 경우 접속이 불가하기 때문이다. 리스트 전체를 입력하는 것을 권장한다.

- acks (세가지 옵션: 0, 1, all)

  acks 옵션을 어떻게 설정하는지에 따라 카프카로 메세지를 전송할 때 메시지 손실 여부와 전송 속도 및 처리량 등이 달라지게 된다.
  - **acks=0: 메시지 손실 가능성이 높지만 빠른 전송이 필요한 경우**<br/>
    카프카 서버에서의 응답을 기다리지 않고, 프로듀서만 준비되면 메시지를 보낸다. 해서, 매우 빠르게 메시지를 보낼 수 있지만, 프로듀서가 카프카로부터 자신이 보낸 메시지에 대한 응답을 기다리지 않기 때문에(ack를 기다리지 않기 때문에) 메시지가 실패했다는 것도 알 수 없기에 손실될 수 있다. retry option을 설정해도 효과를 미칠 수 없다.
  
  - **acks=1: 메시지 손실 가능성이 적고 적당한 속도의 전송이 필요한 경우**<br/>
    프로듀서가 카프카로 메시지를 보낸 후 보낸 메시지를 카프카가 잘 받았는지 acks를 확인한다. 응답 대기 시간 없이 계속 메시지만 보내던 방법과 달리 확인을 기다리는 시간이 추가되어, 메시지 전송 속도는 acks=0에 비해 저하된다. 하지만, 이 ack는 카프카 리더 서버에서 보내진 ack이므로 ack 이후에 리더 서버에서 장애가 발생하고 리플리케이션 정책에 따라 팔로워 중 하나가 다음 리더가 되므로, 전의 리더에 쌓인 메시지를 팔로워들이 가져올 수 없어지는 상황이 발생할 수 있다.
  
  - **acks=all: 전송 속도는 느리지만 메시지 손실이 없어야 하는 경우**<br/>
    프로듀서가 메시지를 전송하고 난 후 리더가 메시지를 받았는지 확인하고 추가로 팔로워까지 메시지를 받았는지 확인하는 옵션이다. 속도적인 측면으로 볼 때, acks 옵션 중에 가장 느리지만 메시지 손실을 허용하지 않을 경우 사용하는 방법이다. 하지만 `acks=all` 만 설정한다고 해서 유실율이 낮다고 보장되는 것은 아니다. 최소 리플리케이션 팩터를 지정하는 옵션인 `min.insync.replicas`도 1 이상으로 지정해줄 때, 그 효과가 나타난다.

## Clients
- Ruby: https://github.com/zendesk/ruby-kafka
