# [Fundamentals of TDD](https://thoughtbot.com/upcase/videos/fundamentals-of-tdd-overview)

1. Red-Green-Refactor
2. Telling a Story with Your Tests

Test-Driven Development is a development technique where you write a failing test and then create code to make that test pass. This process is sometimes called a red-green-refactor cycle with the failing tests being the "red" state, passing tests being the "green" state, and the refactoring step occurring after tests pass, where code can be confidently improved.

The practice of Test-Driven Development over time generates a growing suite of tests that can serve as protection against a regression (the breaking of a previously working feature). Testing first also puts positive design pressure on code, as it influences code to be written to solve the problem at hand (and not to tackle other future problems that may be out of scope, but are tempting to try to solve now). In this way, TDD acts as a workflow hack, promoting incremental, steady progress toward delivery.

There are perceptions that testing is time-consuming, and reduces efficiency, as the writing and maintenance of testing occupies time that could be spent writing new features. While testing does require time to do well, as an code base gets larger and larger, the benefits of being able to quickly and accurately validate that the functionality does what is intended grow.

## Red-Green-Refactor

https://thoughtbot.com/upcase/videos/red-green-refactor-by-example

Let's get into the nuts and bolts of TDD.

In this example, we're going to build a calculator through a test-driven process. For our Ruby tests, we're going to use RSpec, a popular testing library with an expressive DSL and excellent community support. We'll use RSpec's autorun feature during this example to run tests every time we update our files. We don't typically use this feature, but it will make checking our work during the Trail faster.

### Writing the First Test

We'll start by writing a test. RSpec uses nested blocks to group tests together. The outermost block describes the class (`Calculator`), and the next level in describes our method, `#add`. One more level in, and we write the spec for our first behavior inside an `it` block.

```ruby
describe Calculator do
  describe "#add" do
    it "adds two numbers" do
      calculator = Calculator.new

      expect(calculator.add(1, 1)).to eq(2)
    end
  end
end
```

The contents of the spec are mostly the Ruby you already know. RSpec's DSL provides some methods that give your tests some English readability. `#expect` is how you tell RSpec to perform some verification of test results.

### Our First Error: Red

The first run of the test suite gives us an error. This is good! Errors in TDD help us determine what incremental step to take next. The new code should implement the simplest possible logic (within reason) to resolve the error.

First, we add the class, as our error is due to `Calculator` not being defined. Adding the class will then lead to an error about an undefined method `#add`. Implementing `Calculator#add` will then lead to an error about an incorrect number of arguments. Giving `#add` arguments will then lead to an error about the returned value being `nil` rather than the sum. Now it's time to implement our method logic.

```ruby
class Calculator
  def add(a, b)

  end
end
```

### Tests Pass: Green

Hard-coding `#add` to return `15` and make the test pass may seem like a bad idea, but we're not done yet. Now that our test passes, we'll write another test that requires a more generalized solution. A second test exposes our hard-coded return value as an inadequate solution and requires a better implementation to make both tests pass.

It's not always necessary to resolve tests initially through a hard-coded value, but the initial implementation and the quick iteration to a general implementation illustrates how TDD can guide you to the minimum code needed to deliver the feature.

### Implementing the Next Feature: Factorial

With the `#add` method working as we want, it's time to add a new capability to our calculator, to return the result of a [factorial](https://en.wikipedia.org/wiki/Factorial).

Factorial has two cases: factorial for a number is all of the positive integers from one up to that number multiplied by each other. Factorial `0`, the special case, is `1`. We'll write a test to handle each of these cases:

```ruby
describe "#factorial" do
  it "returns 1 when given 0 (0! = 1)" do
    calc = calculator.new

    expect(calc.factorial(0)).to eq(1)
  end

  it "returns 120 when given 5 (5! = 120)" do
    calc = calculator.new

    expect(calc.factorial(5)).to eq(120)
  end
end
```

We'll resolve errors for each of the tests individually, starting with the simplest case, factorial `0`. First, we define the method, then we give the method an argument, then we return the expected result.

```ruby
def factorial(n)
  1
end
```

Our spec passes, and we can move on to the more complicated general case, which is still failing. A recursive solution is straightforward approach, with an `if` clause guarding against the `0` case.

```ruby
def factorial(n)
  if n == 0
    1
  else
    n * factorial(n-1)
  end
end
```

### Refactoring

With passing tests, we're green across the board. This state is a great time to do some refactoring, while your understanding of the code is fresh and your test suite is ready to backstop you against regressions.



## Telling a Story with Your Tests

https://thoughtbot.com/upcase/videos/telling-a-story-with-your-tests

In prior steps we discovered some of the benefits of TDD:

* suite of regression tests (easier changes)
* positive design pressure
* workflow benefit of tackling problem is small steps

But there's another benefit: *tests are automated, living documentation!*

Comments have a problem in that they may be outdated, which makes them worse than no comments at all if they say the wrong thing and inspire false confidence.

###Four Phases of Testing

Tests can tell a story. These stories have four acts, which in test parlance are "phases":

* Setup - get the conditions correct for the test
* Exercise - perform the thing that you're testing
* Verification - verify that the exercise did what you expected
* Teardown - undo any conditions that shouldn't persist post-test

### Test Phases in Action

Let's examine the test phases in an example.

```ruby
describe "#promote_to_admin" do
  it "makes a regular membership an admin membership" do
    # setup
    membership = Membership.new(admin: false)

    # exercise
    membership.promote_to_admin

    # verify
    expect(membership).to be_admin
  end
end
```

(In this test the teardown phase isn't necessary.)

This test breaks its phases into distinct, easily identifiable parts. (You don't need the comments, those are here for emphasis.) It's often a good idea to add a line break between phases to help a developer (who might be you in the future!) to discern the borders of your tests' phases.

The test is also written to be explicit about what's being tested. A new `Membership` is not an admin membership by default, but Harry is setting `admin: false` in the setup phase to help communicate intent about what the test is doing.

## Before, Let, and Mystery Guests

Often tests will obscure what's going on in the name of de-duplication. Here's an RSpec example that leverages a `before` block to execute some test setup and declares some memoized test variables using `#let`:

```ruby
describe Membership do
  before(:each) do
    chocolate_membership.promote_to_admin
  end

  let(:user) { User.new("Bill Wonka") }
  let(:chocolate_group) { Group.new("Chocolate Factory") }
  let(:peach_group) { Group.new("Giant Peach Enthusiasts") }
  let(:chocolate_membership) { Membership.new(user: user, group: chocolate_group, admin: false) }
  let(:peach_membership) { Membership.new(user: user, group: peach_group, admin: false) }

  describe "#promote_to_admin" do
    it "makes a regular membership an admin membership" do
      expect(chocolate_membership).to be_admin
    end

    it "doesn't change other memberships" do
      expect(peach_membership).not_to be_admin
    end
  end
end
```

It can be tempting to employ these RSpec features to avoid duplication in test code, but they can make tests hard to follow and deprive the test of its ability to tell a clear story. `let` in particular can be problematic as the contents of the memoized variable won't be set until the variable is referenced at least once in the test. In the first example, `peach_group` and `peach_membership` doesn't exist yet, as it was never referenced during the test exercise.

DRY is a good principle to follow in code, but it's a means to an end, not the end itself. Often in tests, overly-aggressive de-duplication can lower the quality of test code, as it loses its explanatory capability.

Frequent use of `before` blocks and `let` may be a testing anti-pattern, but that doesn't mean you can't apply any DRY in your tests. Here's an example of a test setup that could be reused in other tests, but retains an explicit setup phase:

```ruby
describe "#promote_to_admin" do
  it "makes a regular membership an admin membership" do
    membership_to_promote = build_non_admin_membership

    membership_to_promote.promote_to_admin

    expect(membership_to_promote).to be_admin
  end

  it "doesn't change other memberships" do
    membership_to_promote = build_non_admin_membership
    membership_to_not_promote = build_non_admin_membership

    membership_to_promote.promote_to_admin

    expect(membership_to_not_promote).not_to be_admin
  end

  def build_non_admin_membership
    user = User.new
    group = Group.new("A group")

    Membership.new(user: user, group: group, admin: false)
  end
end
```

Here basic Ruby methods rather than the RSpec DSL allow for clear declaration of intent along with pulling out complicated or repetitive setup out of the test example.

## Introducing the Unit Converter

https://thoughtbot.com/upcase/videos/introducing-the-unit-converter

Now that we've looked at some small examples using TDD, it's time to jump into a meatier project: building a measurement unit converter.

Getting StartedJump to Topic In Video
To start, we'll pick straightforward examples for `UnitConverter#convert:` the method will help us convert 2 cups into the correct number of liters (0.473 liters for those of you keeping score at home), and will raise an exception if the requested measurement types don't translate from one to the other. These RSpec tests will help us get to the code we want to have:

```ruby
describe UnitConverter do
  describe "#convert" do
    it "translates between objects of the same dimension" do
      converter = UnitConverter.new(2, :cup, :liter)

      expect(converter.convert).to be_within(0.001).of(0.473176)
    end

    it "raises an error if the objects are of differing dimensions" do
      converter = UnitConverter.new(2, :cup, :grams)

      expect { converter.convert }.to raise_error(DimensionalMismatchError)
    end
  end
end
```

Sometimes it can make sense to combine two test phases, as we have here. The exercise phase is so straightforward that storing it in a variable what will immediately be verified in the next step isn't necessary.

In the test that verifies the raising of an exception, note that our exercise is wrapped in a block, which allows RSpec to verify against the specific execution of the block's contents.

Attempting to run the spec informs us the class doesn't exist yet, and subsequently that the constructor has the wrong number of arguments. Once those initial failures are fixed, it's time to drill down and focus on a single example.

### Isolating An Example

Rather than try to solve all the failures at once, it's better to focus on a single test failure, and write the code that makes the spec pass. One way to skip a test is to replace its it invocation with `xit`, which tells RSpec that the example should be considered pending and shouldn't be run in the suite.

```ruby
# skip this example
xit "raises an error if the objects are of differing dimensions" do
  converter = UnitConverter.new(2, :cup, :grams)

  expect { converter.convert }.to raise_error(DimensionalMismatchError)
end
```

### Changing the Converter with Tests

The `UnitConverter` works, but it could be improved if quantities and units were expressed together in a way that made more sense. Ian and Harry want to modify the converter to take a quantity (a data clump combining an amount and a unit) as an argument and to return a quantity. First we'll modify the tests to accommodate the new interface, watch the specs fail, and then we'll update the code to make the specs pass.

### Don't Test Private Methods!

In the `UnitConverter` specs, there are private methods in the class that aren't directly tested in the suite. This coverage decision is intentional! Private methods are an implementation detail that should be able to change in refactoring without breaking tests. Your public methods should be covered by tests, and the behavior of private methods might be covered by tests of public methods, but your private methods should not be tested directly. Don't use `#send` to cheat and invoke private methods for test.

## Refactoring with Test Coverage

https://thoughtbot.com/upcase/videos/refactoring-with-test-coverage

Now that we've built something more involved using TDD, it's time to do some refactoring informed by our test coverage.

### Fixing a Bug

Currently the `UnitConverter` can't convert same units to the same units (i.e. cups to cups). Rather than fixing this problem by adding a same unit-to-same unit mapping and deepening our growing list of unit conversion possibilities, instead we'll refactor the converter to more elegantly handle conversions of units that share the same dimension.

### Trust Me, I'm a Programmer
The refactoring begins with an update to the structure of the `CONVERSION_FACTORS` constant, which supplies the unit-to-unit mappings. As this constant is a private implementation detail, we don't have to modify our existing tests. In fact, they shouldn't have to change at all, as they are our reference to confirm that the converter continues to work as expected.

When refactoring, after each small change, resist the temptation to write the code you expect to be the final implementation. Let the error messages from your tests guide you to the solution. Here Ian and Harry find that the tests help them find a misnamed block variable, which they then update to achieve a green test suite.

### Refactored With Confidence

A good test suite gives you fantastic leverage when you want to perform a refactoring. With tests in place, you can make changes to your code with the assurance that your intended functionality continues to work after your work is completed, protecting against regressions. Without a test suite, refactorings are much riskier, as each change may introduce subtle bugs, particularly ones that have already been fixed in previous revisions.


-

### Additional Resources

[XUnitPatterns.com](http://xunitpatterns.com) - xUnit Test Patterns: Refactoring Test Code

[Let's Not](https://robots.thoughtbot.com/lets-not) - A Giant Robots post about mystery guests
