# Glossary

<br>
# D

### Database Migration
<abbr title='database'>Database</abbr> migration is the process of transferring data between storage types, formats, or computer systems. It is a key consideration for any system implementation, upgrade, or consolidation. Database migration is usually performed programmatically to achieve an automated migration, freeing up human resources from tedious tasks

### Double (Mock)
A simple object that's preprogrammed with expectations and responses as preparation for the calls that it will receive.
 
```
ruby new_car = double(Car.new)
```
<br>
# E

### Encapsulation
Encapsulation means that the internal representation of an object is hidden from the outside. Only the object can interact with its internal data. Public methods can be created to open a defined way to access the logic inside an object.

<br>
# G

### `GET`
It is a HTTP protocol that is used to retrieve remote data.

<br>
# I

### Inheritance
Inheritance is a relation between two classes. A child class inherits all the features of its parent class. Methods from the parent can be overridden in the child and new logic can be added. However a certain form of multi-inheritance can be replicated through the use of modules as mix-ins.

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
# N

### `psql`
It is the interactive terminal for working with Postgres (similar to Ruby's irb).

<br>
# O

### Object Relational Mapping
ORM (O/RM or O/R mapping tool), in computer science, is a programming technique for converting data between incompatible type systems in object-oriented programming languages.

<br>
# P

### `POST`
It is a HTTP protocol that is used to insert/update remote data.

<br>
# R

### RTFM
Read the fucking manual. 🙃

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

<br>
# Y

### YAGNI
"You aren't gonna need it" is a principle of extreme programming (XP) that states a programmer should not add functionality until deemed necessary.
