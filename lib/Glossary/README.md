# Glossary

## D

* __Double__ (Mock)__:__ A simple object that's preprogrammed with expectations and responses as preparation for the calls that it will receive.
 
```
ruby new_car = double(Car.new)
```

## M

* __Memoization:__  If we already have a value for the instance variable, use it. If not, then go get a new value, and assign it to the instance variable.
  
```ruby
def car
  @car ||= Car.new
end
```

## S

* __Stub:__ An instruction to an object to return a specific response to a method call.

```ruby
allow(car).to receive(brake)

```
