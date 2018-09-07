# How sessions work in Ruby on Rails
[HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)는 [stateless protocol](https://en.wikipedia.org/wiki/Stateless_protocol)이다. 이전 request로부터 얻은 정보로 현재 request를 처리할 수 없다. web은 로그인 기능이 필수이다. http protocol 만으로는 이 기능들을 구현할 수 없으며, session/cookie라는 개념이 등장하게 되었다. 웹 브라우저와 서버 간의 semi-permanent connection이다.

## Session & Cookie
### Session
일정 시간동안 같은 브라우저로 부터 들어오는 requests를 하나의 상태로 보고 그 상태를 유지하는 기술.

웹 서버에 접속한 이후로 브라우저를 종료할 때 까지 유지되는 상태. 서버 사이드의 Storage.

이때, 클라이언트가 request를 보내면, 서버의 엔진이 클라이언트에게 ID를 부여하며 이를 session id라고 부른다.

브라우저가 종료되면 session id는 바로 파기된다.

### Cookie
클라이언트 로컬에 저장되는 key/value로 구성된 데이터 파일이다.

쇼핑몰 장바구니, 자동로그인 등에 활용된다.

로컬에 저장되기 때문에, 변질되거나 request에서 스나이핑 당할 우려가 있어 세션에 비해 보안에 취약하다.

저장되는 '일정 시간'이 있지만, 파일로 저장되기 때문에 브라우저를 종료해도 계속 정보가 남아있을 수 있다.

## Signing in

1. 브라우저 접속
2. Session ID 발급
3. 쿠키에 session id 저장
4. 그 이후의 request에 대해서는 session id 값을 같이 서버에 전달
5. 로그인 유지

## on Rails!
```ruby
$ rails generate controller Sessions new
```

```
create  app/controllers/sessions_controller.rb
route  get 'sessions/new'
invoke  erb
create    app/views/sessions
create    app/views/sessions/new.html.erb
invoke  test_unit
create    test/controllers/sessions_controller_test.rb
invoke  helper
create    app/helpers/sessions_helper.rb
invoke    test_unit
invoke  assets
invoke    coffee
create      app/assets/javascripts/sessions.coffee
invoke    scss
create      app/assets/stylesheets/sessions.scss
```

### Page Hierarchy
#### app/views/sessions/new.html
- 로그인 페이지

#### app/controllers/sessions_controller.rb
- 세션 컨트롤러. 로그인, 로그아웃 등

### With [devise](https://github.com/plataformatec/devise)
Refer https://github.com/aria-grande/TIL/blob/master/Rails/devise.md

## Refer
- https://www.railstutorial.org/book/basic_login
