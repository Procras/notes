# Glossary

## D

### Double(Mock)
A simple object that's preprogrammed with expectations and responses as preparation for the calls that it will receive.
 
```
ruby new_car = double(Car.new)
```

## M

### Memoization
If we already have a value for the instance variable, use it. If not, then go get a new value, and assign it to the instance variable.
  
```ruby
def car
  @car ||= Car.new
end
```

## S

### Spyies 
They are like test doubles with a tape recorder turned on. They keep track for the messages that are received so that you can look back at the messages after the fact, in your expectations.

### Stub
An instruction to an object to return a specific response to a method call.

```ruby
allow(car).to receive(brake).and_return('Slowing down')

```
