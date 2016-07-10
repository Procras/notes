## 2) Objects, methods and local variables

### 2.1) Talking to objects

When you want something to be done, you ask an object to do it. Rather than ask in the abstract whether `a` *equals* `b`, you ask `a` whether it considers itself equal to `b`. 

#### 2.1.1) Ruby and onject orientation

In object-oriented programming (OOP), you perform calculations, data manipulation, and input/output operations by creating objects and asking them to perform actions and provide you with information.

In most object-oriented languages, including Ruby, every objectos an example or instance of a particular class, and the behaviour of individual objects is determined at least to some extent by the method definitions present in the object's class.

#### 2.1.3) Methods that take arguments

The variables listed in the method definition are the method's *formal parameters*, and values you supply to the method when you call it are the correspondint *arguments*. (It's comman to use the workd *arguments*, indormally, to refer to a method's parameters as well as a method call's arguments, but it's usefull to know the technical distinction.)

#### 2.1.4) The return value of a method

Every method call is an expression. When you call a method, the method call evaluates to a something. THis result of calling a method is the method's *return value*.

### 2.2) Crafting an object: The behaviour of a ticket

#### 2.2.4) Expressing Boolean state in a method

Every expression in Ruby ecaluates to an object, and every object in Ruby has a truth value. The truth value of almost every object in Ruby is `true`. The only onjects whose truth value (or Boolean value) is `false` are the object `false` and the special nonentity `nil`.

In case where the `puts` happens, the whole ecpression evaluates to `nil`-because the return value of `puts` is always `nil`. Remembering that `nil` has a Boolean value of `false`, you can get into acrobatics with irb. If you put `puts` in an `if` clause, the clause will be false, but it will still be evaluated.

### 2.3) The innate behaviours of an object

Every object is 'born' with certain innate abilities. To see a list of innate methods, yuo can call the `methods` method.

#### 2.3.1) Identifying objects uniquely with the `object_id` method

* `.object_id`
 
#### 2.3.2) Querying an object's abilities with `respond_to?` method

`respond_to?` method exist for all objects; you can ask any object whether it responds to any message.

`respond_to?` is an ecample of *introspection* or *reflection*, two terms that refer to examining the state of a program while it's running.

#### 2.3.3) Sending messages to objects with the send method

```
print 'Info desired:'
request = gets.chomp

if request == 'venue'
  puts ticket.venue
if request == 'performer'
  puts ticket.performer
...
```

Alternatively; you can send the word directly to the `ticket` object.

```
if ticket.respond_to?(request)
  puts ticket.send(request)
else
  puts 'No info available'
end
```

# p.48
### 2.4) A close look at method arguments

#### 2.5.4) Local variables and the things that look like them

When Ruby sees a plain word sittin there -a bareword identifier, like `s`, `ticket`, `puts` or `user_name`- it interprets it as one of three things:

* A local variable
* A keyword
* A method call
 
*Keywords* are special reserverd words that you can't use as variable names.

Like local variables, method calls can be plain words. If the method call inclueds arguments in parentheses -or even empty parentheses- then it's clear that it's not a local variable. In other cases, there may be some ambigiuty, and Ruby has to figure it out.

 Here's how Ruby decides what it's seeing when it encounters a plain identifier:
 
 1. If the identifier is a keyword, it's a keyword (Ruby has an internal list of these and recognizes them).
 2. If there's an equal sign (=) to the right of the identifier, it's a local variable undergoing an assigment.
 3. Otherwise, the identifiers is assumed to be a method call.

 
If you use an identifier that isn't any of there three things, then RUby will pomplain and halt executuon with fatal error. The error message you get when this happens is instructive:

```
$ ruby -e "x"
-e:1:in `<main>`: undefined local variable or method 'x' for main:Object (NameError)
```

Note that Ruby can't tell whether you thought x was a variable or a method. It knows that x isn't a keyword, but it could be either of the other two. So the error message includes both.
