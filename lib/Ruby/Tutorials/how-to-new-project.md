# How Start a New Ruby Project?

### TDD Thinking

|First|Second|Third|
|---|---|---|
|Feature Test|Unit Test|App|
|Capybara|Rspec|Ruby|
|`./spec/features/...`|`./spec/...`|`./lib/...`|

### 5 Steps to Happiness

* Add a Gemfile for dependencies using `bundle init`.
* Inside the Gemfile, add the dependencies.

```ruby
# In Gemfile
source 'https://rubygems.org'

gem 'sinatra'
gem 'rspec-sinatra'
gem 'capybara'

# etc ...
```

* Use `bundle install` to install those dependencies to the project (generating a Gemfile.lock).
* Initialize the app with `rspec-sinatra init --app AppName app.rb`.
* Add `lib` and `features` directories.
```
.
└── directory_name/
    │
    ├── spec/
    │   └── spec_helper.rb
    │   └── features/
    │   │   └── some_feature_spec.rb
    │   │   └── some_more_feature_spec.rb
    │
    │
    ├── view/
    │   └── index.erb
    │
    ├── lib/
    │   └── some_feature.rb
    │   └── some_more_feature.rb
    │
    ├── app.rb
    │
    ├── .rspec
    │
    ├── Gemfile
    ├── Gemfile.lock
    │
    └── config.ru
```
