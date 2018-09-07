# [Devise](https://github.com/plataformatec/devise)
Rails를 위한, Authentication Library

## What is offered?
* Database Authenticatable: hashes and stores a password in the database to validate the authenticity of a user while signing in. The authentication can be done both through POST requests or HTTP Basic Authentication.
* Omniauthable: adds OmniAuth (https://github.com/intridea/omniauth) support.
* Confirmable: sends emails with confirmation instructions and verifies whether an account is already confirmed during sign in.
* Recoverable: resets the user password and sends reset instructions.
* Registerable: handles signing up users through a registration process, also allowing them to edit and destroy their account.
* Rememberable: manages generating and clearing a token for remembering the user from a saved cookie.
* Trackable: tracks sign in count, timestamps and IP address.
* Timeoutable: expires sessions that have not been active in a specified period of time.
* Validatable: provides validations of email and password. It's optional and can be customized, so you're able to define your own validations.
* Lockable: locks an account after a specified number of failed sign-in attempts. Can unlock via email or after a specified time period.

- PasswordController is used for password resetting when a user is not signed in. If user signed in, it redirects you to the root path.

- Flexible authentication solution for Rails with Warden.

## Configure
### Configuring models
```ruby
rails g devise user
```

```
invoke  active_record
create    db/migrate/20180907054047_add_devise_to_users.rb
insert    app/models/user.rb
route  devise_for :users
```

### Configuring controllers
```ruby
rails g devise:controller user
```

```
create  app/controllers/user/confirmations_controller.rb
create  app/controllers/user/passwords_controller.rb
create  app/controllers/user/registrations_controller.rb
create  app/controllers/user/sessions_controller.rb
create  app/controllers/user/unlocks_controller.rb
create  app/controllers/user/omniauth_callbacks_controller.rb
```

### Configuring views
```ruby
rails g devise:views
```

```
invoke  Devise::Generators::SharedViewsGenerator
create    app/views/devise/shared
create    app/views/devise/shared/_links.html.erb
invoke  form_for
create    app/views/devise/confirmations
create    app/views/devise/confirmations/new.html.erb
create    app/views/devise/passwords
create    app/views/devise/passwords/edit.html.erb
create    app/views/devise/passwords/new.html.erb
create    app/views/devise/registrations
create    app/views/devise/registrations/edit.html.erb
create    app/views/devise/registrations/new.html.erb
create    app/views/devise/sessions
create    app/views/devise/sessions/new.html.erb
create    app/views/devise/unlocks
create    app/views/devise/unlocks/new.html.erb
invoke  erb
create    app/views/devise/mailer
create    app/views/devise/mailer/confirmation_instructions.html.erb
create    app/views/devise/mailer/email_changed.html.erb
create    app/views/devise/mailer/password_change.html.erb
create    app/views/devise/mailer/reset_password_instructions.html.erb
create    app/views/devise/mailer/unlock_instructions.html.erb

```

### [Configuring routes](https://github.com/plataformatec/devise#configuring-routes)
```ruby
# routes.rb
devise_for :users, path: 'auth', path_names: { sign_in: 'login', sign_out: 'logout', password: 'secret', confirmation: 'verification', unlock: 'unblock', registration: 'register', sign_up: 'cmon_let_me_in' }
```

## Scope 별로 다른 Authentication 적용하기
http://climber2002.github.io/blog/2015/03/29/customize-devise-to-support-subdomain-authentication/

## Flash: Render Error messages when failed to log in
Definition
- http://api.rubyonrails.org/classes/ActionDispatch/Flash.html

Means in detail
- http://stackoverflow.com/questions/23453538/what-is-flash-hash-in-ruby-on-rails
- http://stackoverflow.com/a/10449095


## [I18n](https://github.com/plataformatec/devise#i18n)
- https://github.com/plataformatec/devise/wiki/I18n

Customize your own I18n solution.
One easy way is to overwrite app/helpers/devise_helper.rb, which is mentioned as “A simple way to show error messages for the current devise resource. If you need to customize this method, you can either overwrite it in your application helpers or copy the views to your application.” in the comment.
