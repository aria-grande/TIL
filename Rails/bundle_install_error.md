# 문제
아래와 같은 메세지를 뿜어내며 `bundle install`이 되지 않았다.

```sh
Fetching mysql2 0.4.10
Installing mysql2 0.4.10 with native extensions
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /Users/areeoh/Desktop/Workspace/Parking/RoadSter/vendor/ruby/2.5.0/gems/mysql2-0.4.10/ext/mysql2
/usr/local/var/rbenv/versions/2.5.1/bin/ruby -r ./siteconf20181019-3655-7pgbj4.rb extconf.rb --with-mysql-config=/usr/local/Cellar/mysql/5.7.17/bin/mysql_config
checking for rb_absint_size()... yes
checking for rb_absint_singlebit_p()... yes
checking for ruby/thread.h... yes
checking for rb_thread_call_without_gvl() in ruby/thread.h... yes
checking for rb_thread_blocking_region()... no
checking for rb_wait_for_single_fd()... yes
checking for rb_hash_dup()... yes
checking for rb_intern3()... yes
checking for rb_big_cmp()... yes
-----
Using mysql_config at /usr/local/Cellar/mysql/5.7.17/bin/mysql_config
-----
checking for mysql.h... yes
checking for errmsg.h... yes
checking for SSL_MODE_DISABLED in mysql.h... yes
checking for SSL_MODE_PREFERRED in mysql.h... yes
checking for SSL_MODE_REQUIRED in mysql.h... yes
checking for SSL_MODE_VERIFY_CA in mysql.h... yes
checking for SSL_MODE_VERIFY_IDENTITY in mysql.h... yes
checking for MYSQL.net.vio in mysql.h... yes
checking for MYSQL.net.pvio in mysql.h... no
checking for MYSQL_ENABLE_CLEARTEXT_PLUGIN in mysql.h... yes
-----
Don't know how to set rpath on your system, if MySQL libraries are not in path mysql2 may not load
-----
-----
Setting libpath to /usr/local/Cellar/mysql/5.7.17/lib
-----
creating Makefile

current directory: /Users/areeoh/Desktop/Workspace/Parking/RoadSter/vendor/ruby/2.5.0/gems/mysql2-0.4.10/ext/mysql2
make "DESTDIR=" clean

current directory: /Users/areeoh/Desktop/Workspace/Parking/RoadSter/vendor/ruby/2.5.0/gems/mysql2-0.4.10/ext/mysql2
make "DESTDIR="
compiling client.c
compiling infile.c
compiling mysql2_ext.c
compiling result.c
result.c:326:40: warning: incompatible pointer types assigning to 'my_bool *' (aka 'char *') from 'bool *' [-Wincompatible-pointer-types]
    wrapper->result_buffers[i].is_null = &wrapper->is_null[i];
                                       ^ ~~~~~~~~~~~~~~~~~~~~
result.c:328:40: warning: incompatible pointer types assigning to 'my_bool *' (aka 'char *') from 'bool *' [-Wincompatible-pointer-types]
    wrapper->result_buffers[i].error   = &wrapper->error[i];
                                       ^ ~~~~~~~~~~~~~~~~~~
2 warnings generated.
compiling statement.c
linking shared-object mysql2/mysql2.bundle
ld: library not found for -lssl
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make: *** [mysql2.bundle] Error 1

make failed, exit code 2

Gem files will remain installed in /Users/areeoh/Desktop/Workspace/Parking/RoadSter/vendor/ruby/2.5.0/gems/mysql2-0.4.10 for inspection.
Results logged to /Users/areeoh/Desktop/Workspace/Parking/RoadSter/vendor/ruby/2.5.0/extensions/x86_64-darwin-17/2.5.0-static/mysql2-0.4.10/gem_make.out

An error occurred while installing mysql2 (0.4.10), and Bundler cannot continue.
Make sure that `gem install mysql2 -v '0.4.10' --source 'https://rubygems.org/'` succeeds before bundling.
```

## 삽질
- `gem pristine -all`로 전부 gem 재설치 후 `bundle install`해도 에러 발생.
- 다른 discussion에서 많이들 해결했다던 `xcode-select --install` 커맨드도 입력해보았으나, 난 이미 install/update가 되어 있어서 별 소용이 없었음.
- config가 잘못되어있나 하여 ` gem install mysql2 -- --with-mysql-config=/usr/local/mysql-5.7.17-macos10.12-x86_64/bin/mysql_config` 시스템에 설치되어 있는 환경 설정을 이용하도록 설치 해도 소용이 없었음.
- 에러메세지를 자세히 읽어보면 **ld: library not found for -lssl**가 있다. `openssl` 라이브러리길래, `brew install openssl`후 `bundle install`을 해도 소용이 없다!!
- 멘붕쓰..

# 해결
- openssl 설치만 해서 되지 않고, LIBRARY_PATH를 export 해줘야 한다.

```sh
brew install openssl
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/opt/openssl/lib/
```

- 참고: https://github.com/brianmario/mysql2/issues/795
