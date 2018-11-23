# 도커 컨테이너의 네트워크 모드
도커의 컨테이너는 서로 연결될 수도 있고, 연결되지 않을 수도 있다. 
컨테이너를 생성할 때 지원되는 네트워크 방식은 크게 4가지가 있다.

브릿지 모드가 디폴트이고, 그 외 모드는 따로 설정을 해줘야 한다.
보안상 브릿지 모드를 권장하고 있다.

## [브릿지 모드](https://docs.docker.com/network/bridge/)
네트워크에서의 브릿지 네트워크(Bridge network)는 네트워크 세그먼트 간의 트래픽을 전달하는 연결 레이어이며, 호스트의 커널 내에서 돌아가는 하드웨어 혹은 소프트웨어 디바이스가 될 수 있다.
도커에서의 브릿지 네트워크는 software bridge이다. 

- docker daemon을 실행하면 먼저 docker0이라는 브릿지가 생성된다. 
- 컨테이너를 생성하면, 각 컨테이너마다 고유한 network namespace 영역이 하나씩 생성이 되고, docker0 bridge에 컨테이너의 인터페이스들이 하나씩 바인딩 되는 구조이다. 
- 컨테이너는 docker-proxy라는 데몬을 통해 호스트와 연결되며, 기본적으로는 호스트와 격리된 상태이다.

아래 명령어로 확인해볼 수 있다.
```sh
$ docker network inspect bridge
[
    {
        "Name": "bridge",
        "Id": "ba7229ab294aa78401ca6bd4f1427164c0962f5ae30e1b503f70886278002e18",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "10.xxx.xxx.xxx/16",
                    "Gateway": "10.xxx.xxx.xxx"
                }
            ]
        },
        "Internal": false,
        "Containers": {
            "ed7bd6ee7d2bee481321c7f3f7c80167ae4e552a1b89d3575bc2f7baeb7de574": {
                "Name": "container_name",
                "EndpointID": "blahblahblah",
                "MacAddress": "XX:XX:XX:XX:XX:XX",
                "IPv4Address": "10.xxx.xxx.xxx/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```


## [호스트 모드](https://docs.docker.com/network/host/)
컨테이너가 독립적인 네트워크 영역을 갖지 않고 도커 호스트와 네트워크를 함께 사용하게 된다.(네트워크 외 다른 환경은 동일)

만약 컨테이너를 호스트 모드 + 80번 포트로 연결한다면, 컨테이너는 호스트 IP 주소의 80번 포트에서도 접근 가능하게 된다. **네트워크가 분리/고립되지 않는다!**

고로 호스트 모드로 동작하고 있는 컨테이너에서 보안문제가 발생했을 경우, 다른 컨테이너/호스트에 공격을 시도할 수 있게 되므로 사용에 유의해야 한다.

host 옵션으로 생성된 컨테이너는 bridge를 사용하지 않으므로 docker0에 바인딩 되지 않는다.
```sh
$ docker network inspect bridge
[
    {
        "Name": "host",
        "Id": "ba7229ab294aa78401ca6bd4f1427164c0962f5ae30e1b503f70886278002e18",
        "Scope": "local",
        "Driver": "host",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": []
        },
        "Internal": false,
        "Containers": {
            "ed7bd6ee7d2bee481321c7f3f7c80167ae4e552a1b89d3575bc2f7baeb7de574": {
                "Name": "container_name",
                "EndpointID": "blahblahblah",
                "MacAddress": "",
                "IPv4Address": "",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
```

