# Glossary

## M

* __Memoization:__  If we already have a value for the instance variable, use it. If not, then go get a new value, and assign it to the instance variable.
  
```ruby
def car
  @car ||= Car.new
end
```
