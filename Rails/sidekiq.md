# [Sidekiq](https://github.com/mperham/sidekiq)
Rails에서 쉽게 사용 할 수 있는 background process!

## 구성
<img src="https://brandonhilkert.com/images/sidekiq/rails-web-worker.png" width="400"/>

### Client
루비 프로세스 안에서 돌며, application 내에 job을 생성하게 해준다.

### Redis
Queue, Data storage. runtime 동안 모든 job의 데이터를 홀딩하고 있다.

### Server
Redis의 큐에서 job을 pull & process.


## 기능
### Job
- `perform_now`

  Rails server에서 바로 실행.

- `perform_async`

  sidekiq(redis)를 통해 비동기적으로 실행.
  
  [Make your job parameters small and simple](https://github.com/mperham/sidekiq/wiki/Best-Practices#1-make-your-job-parameters-small-and-simple)
```
NO STATE IN PARAMETER!
perform_async를 통해 전달되는 arguments는 simple JSON datatypes로 구성되어야 한다.
Sidekiq client가 Redis로 데이터를 보내기 위해 JSON.dump를 하고, 
Sidekiq server에서는 JSON.load로 데이터를 로드하기 때문이다.
symbol이나 ruby objects은 제대로 처리되지 않을 수 있으니 사용하지 말자.
```

### Cron
schedule.yml 파일 내에 크론 스케줄을 입력하고
```yml
expireCoupon:
  cron: "0 0 * * *"
  class: "ExpireCouponsJob"
  queue: default
```
sidekiq 설정 파일(sidekiq.rb)에 아래와 같이 스케줄 파일을 로드한다.
```ruby
schedule_file = 'config/schedule.yml'

if File.exists?(schedule_file) && Sidekiq.server?
  Sidekiq::Cron::Job.load_from_hash YAML.load_file(schedule_file)
end
```

## Job과 Worker
### [ActiveJob](https://github.com/mperham/sidekiq/wiki/Active+Job)
ActiveJob은 Rails에서 제공하는 표준 인터페이스이다. sidekiq에서 제공하는 것이 아님.
따라서 ActiveJob의 adapter는 반드시 sidekiq으로 설정해야 한다.

### [Worker](https://github.com/mperham/sidekiq/wiki/Advanced-Options#workers)
sidekiq에서 제공하는 feature


## Sharding
_Sidekiq 3.0 이상 제공_
단일 Redis server로 처리할 수 없을 때, ConnectionPool을 여러개 만들어 sharding을 할 수 있다. 아직 한계점이 여러 존재함.

https://github.com/mperham/sidekiq/wiki/Sharding
