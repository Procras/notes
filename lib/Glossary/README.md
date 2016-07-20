# Glossary

<br>
# D

### Double (Mock)
A simple object that's preprogrammed with expectations and responses as preparation for the calls that it will receive.
 
```
ruby new_car = double(Car.new)
```

<br>
# M

### Memoization
If we already have a value for the instance variable, use it. If not, then go get a new value, and assign it to the instance variable.
  
```ruby
def car
  @car ||= Car.new
end
```

<br>
# S

### Spyies 
They are like test doubles with a tape recorder turned on. They keep track for the messages that are received so that you can look back at the messages after the fact, in your expectations.

### Stub
An instruction to an object to return a specific response to a method call.

```ruby
allow(car).to receive(brake).and_return('Slowing down')
```

<br>
# U

### User stories
User stories are short, simple descriptions of a feature told from the perspective of the person who desires the new capability, usually a user or customer of the system. They typically follow a simple template:

```
As a <type of user>, I want <some goal> so that <some reason>.
```

User stories are often written on index cards or sticky notes, stored in a shoe box, and arranged on walls or tables to facilitate planning and discussion. As such, they strongly shift the focus from writing about features to discussing them. In fact, these discussions are more important than whatever text is written.
