# [CanCan](https://github.com/ryanb/cancan)
Rails를 위한 권한 관리 라이브러리 이다.

## Situation
ApplicationController에 `authorize_resource`가 있다.
PicksController는 ApplicationController를 상속받고 있다.
PicksController 하위의 메소드들에 대해 authorization 과정이 수행되지 않고 있다.
```ruby
class  ApplicationController
  authorize_resource
  
  ...
end
```
```ruby
class PicksController < ApplicationController
  def index
    ...
  end
end
```

## 원인
authorize_resource는 간략하게 `before_action :authorize!` 정도로 나타낼 수 있다.
```ruby
authorize!(params[:action].to_sym, @article || Article)
```

authorize를 하기 위해서는 resource를 load하는 것이 선행 되어야 한다.
```ruby
def load_resource
  return if skip?(:load)
  if load_instance?
    self.resource_instance ||= load_resource_instance
  elsif load_collection?
    self.collection_instance ||= load_collection
  end
end
```

## 해결
Roadster의 파트너용 컨트롤러들은 load_resource를 하는 방식이 각 리소스마다 다른 환경이므로 두 가지 방법으로 해결 할 수 있다.

방법 1. 각 컨트롤러마다 `load_and_authorize_resource` 및 옵션 명시
```ruby
class PicksController < ApplicationController
  # resource 조회 시, 기본적으로 Pick.find_by_id(param[:id])를 하고 있으므로, find_by 옵션과 id_param 옵션을 명시.
  # singleton: Pass true if this is a singleton resource through a has_one association.
  load_and_authorize_resource find_by: :token, id_param: :token, singleton: true
end
```

방법 2. 각 컨트롤러마다 `authorize!` 수동 실행
```ruby
class PicksController < ApplicationController
  before_action :authorize_pick
  
  def authorize_pick
    @pick = Pick.find_by_token(params[:token])
    authorize!(:manage, @pick)
  end
  
  ...
end
```

## Reference
- https://github.com/CanCanCommunity/cancancan/wiki/Non-RESTful-Controllers
- https://github.com/ryanb/cancan/wiki/authorizing-controller-actions
