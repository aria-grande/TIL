# Load Balancer

## [Load Balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing))
부하 분산. 대용량 트래픽을 장애 없이 처리하기 위해 여러 대의 서버에 트래픽을 분배하는 기술.<br/>
Application Server 앞 단에 위치하며, 한 서버가 다운되더라도 정상 동작하는 다른 서버에 트래픽을 전달한다.<br/>
Hardware LB와 Software LB가 존재한다.<br/>
웹서버들은 Private IP로 구성되는 경우가 많다. 로드 밸런서는 public network와 private network의 경계에 있는데, public network와 통신할 수 있는 VIP를 가진다.클라이언트가 VIP로 접근하면, 로드 밸런서는 지정한 알고리즘에 따라서 트래픽을 분산한다.

<br/>
## Load Balancing Algorithms
### [Round Robin](https://www.nginx.com/resources/glossary/round-robin-load-balancing/)
순차적으로 서버에 분산 된다.
간단한 수준의 분산 알고리즘이다.

### Least Connections
Request 시점에 클라이언트와 가장 적게 연결을 맺고 있는 서버에 트래픽을 전달한다.

### IP Hash
클라이언트의 IP에 따라 어떤 서버에 트래픽을 전달할지 결정한다.

<br/><br/>

## 사용되는 기술
### NAT(Network Address Translation)
Private IP를 Virtual IP로 바꿔주는 주소 변조기

### DSR(Dynamic Source Routing protocol)
서버에서 클라이언트로 되돌아갈 때, destination IP를 스위치의 IP 주소가 아닌 클라이언트의 IP 주소로 전달해서, 네트워크 스위치를 거치지 않고 클라이언트에게 응답할 수 있다.

### Tunneling
터널. 데이터를 캡슐화해서 연결된 상호 간에만 터널을 만들어 통신을 하며, 캡슐화된 패킷을 구별 및 해제할 수 있다.

<br/><br/>
## 예
### [Nginx](http://nginx.org/)
[Nginx as load balancer](http://nginx.org/en/docs/http/load_balancing.html)

### [HAProxy](http://www.haproxy.org/)
안정적이고 고성능인 TCP/HTTP 로드밸런서용 proxy.

#### Reverse Proxy
실제 서버 요청에 대해서 앞 단에 존재하며, 서버로 들어오는 요청을 대신 받아서 전달하고 클라이언트에 그 결과를 다시 전달하는 프록시이다.
##### Reverse proxy vs forward proxy
https://www.thegeekstuff.com/2016/01/load-balancer-intro/

<hr/>

## 참고 링크
- [Introduction of load balancer](https://www.thegeekstuff.com/2016/01/load-balancer-intro/)
- [Introduction to haproxy and load-balancing concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)
