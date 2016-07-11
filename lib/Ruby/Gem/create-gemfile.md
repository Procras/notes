# Create a Gemfile

If Bundler is installed:

1. Use Bundler to create a Gemfile: `bundle init`

2. Add Ruby version: `ruby '2.2.3'`

3. Add names of Gems: `gem "rspec"`

4. Invoke bundler: `bundle`

5. Commit these files and push it to Github.
  * `git add Gemfile`
  * `git add Gemfile.lock`
  * `git commit -m 'Closing #1: added a Gemfile'`
  * `git push origin master`

  
Example:
 
```
source "https://rubygems.org"

ruby '2.2.3'

group :development, :test do
 gem "rspec"
end
```
