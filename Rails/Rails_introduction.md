# Ruby on Rails
- Rails is a web application development framework written in Ruby.

## Rails way
- **Don't repeat yourself**: maintainable, more extensible, and less buggy.
- **Convention Over Configuration**: Rails has opinions about the best way to do many things in a web application, and defaults to this set of conventions, rather than require that you specify endless configuration files.

## Rails features
### [Rails CLI](https://guides.rubyonrails.org/command_line.html)

## Architecture
- Rails uses Model-View-Controller(MVC) architectural pattern in order to improve the maintainability of the application.

![rails architecture](https://csharpcorner-mindcrackerinc.netdna-ssl.com/article/generate-a-controller-and-view-in-ruby-on-rails/Images/image011.jpg)

### Model
- Model layer carries the business logic of the application and the rules to manipulate the data.
- Represented as a table in database.
- supported by [ActiveRecord](https://guides.rorlab.org/active_record_basics.html).

### View
- front-end of the application, representing the user interface.
- HTML files with embedded Ruby code.
- [layouts and rendering in Rails](https://guides.rorlab.org/layouts_and_rendering.html)

### Controller
- interact with models and views.
- The incoming requests from the browsers are processed by the controllers, which process the data from the models and pass it to the views for presentation.
- supported by [ActionController](https://guides.rubyonrails.org/action_controller_overview.html)

## [Directories](https://www.sitepoint.com/a-quick-study-of-the-rails-directory-structure/)
### [Gemfile](https://bundler.io/gemfile.html)
- bundler managing dependencies to run your application.
### package.json
- javascript package manager using [yarn](https://yarnpkg.com/en/)
- install packages using command `yarn install`

### app/
- application folder

#### app/assets/
- static files required for the application's front-end grouped.
- JS, CSS, fonts, images, ...

#### app/models/
- model files/
##### app/models/concenrs
- containing methods that might be used in multiple model files.

#### app/controllers/
- controller files.

#### app/views/
- convention: {controller_name}/{action_name}.html.erb
##### app/views/layouts
- layout in specific view

#### app/helpers/
- helpef functions for views reside.
- convention: {controller_name}_helper.rb

### bin/
- wrappers to run the gem executables scoped to your application.
- rails, rake... execution files of ruby script.
```
bin/rails console
```

### config/
- route, database, enviornment settings.
#### config/database.yml
- configuration for database connection
#### routes.rb
- managing request routing
#### config/environments/
- rails can configure multiple environments and configurations of them.
#### config.locales/
- storage of interpretation of error messages, attributes, enums, …

### db/
- db schema histories.

### lib/
- extension libraries

### log/
- logs

### public/
- static assets not powered by routes.rb

### test/
- test codes.

### tmp/
- tempeorary files such as cache, session files, pid.

### vendor/
- third-party codes.
