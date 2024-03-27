---
title: Testing
teaching: 35
exercises: 25
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why test?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the place of testing in a scientific workflow.
- Understand that testing has many forms.

::::::::::::::::::::::::::::::::::::::::::::::::

## Basics of testing

The first step toward getting the right answers from our programs is to assume
that mistakes *will* happen and to guard against them.  This is called
**defensive programming** and the most common way to do it is to add alarms and
tests into our code so that it checks itself.

**Testing** should be a seamless part of scientific software development process.
This is analogous to experiment design in the experimental science world:

- At the beginning of a new project, tests can be used to help guide the 
  overall architecture of the project.
- The act of writing tests can help clarify how the software should be perform when you are done. 
- In fact, starting to write the tests _before_ you even write the software 
  might be advisable. Such a practice is called _test-driven development_.

## Tests types

There are many ways to test software, such as:

- Assertions
- Exceptions
- Unit Tests
- Integration Tests

*Exceptions and Assertions*: While writing code, `exceptions` and `assertions` 
can be added to sound an alarm as runtime problems come up. These kinds of 
tests, are embedded in the software itself and handle, as their name implies, 
exceptional cases rather than the norm. 

*Unit Tests*: Unit tests investigate the behavior of units of code (such as
functions, classes, or data structures), ideally the smallest possible units.
By validating each software unit across the valid range of its input and output
parameters, tracking down unexpected behavior that may appear when the units are
combined is made vastly simpler.

*Integration Tests*: Integration tests check that various pieces of the
software work together as expected. They can be both on small scales, or system wide.

::::::::::::::::::::::::::::::::::::: callout

### How much testing is enough?

Possible tests metrics are:

- Lines of code.
- Test coverage [example](https://sonarcloud.io/component_measures?id=eWaterCycle_ewatercycle&metric=coverage&view=treemap&selected=eWaterCycle_ewatercycle%3Aewatercycle): to check to which extent the software is being coverted by the tests.

::::::::::::::::::::::::::::::::::::::::::::::::

## PyTest

Currently, [PyTest](docs.pytest.org) is the recommended Python testing framework. Let's see how it can be used to run the tests.

First, create a directory and navigate into it:

```bash
mkdir pytest-example
cd pytest-example
```

Then, create a file `example.py` containing an example test. You can use for favourite text editor for creating the file:

```bash
nano example.py
```

And then, in the file, type:

```python
def add(a, b):
   return a + b
 
 
def test_add():  # Special name!
    assert add(2, 3) == 5  # What's `assert`? 🤔
    assert add('space', 'ship') == 'spaceship'

```

::::::::::::::::::::::::::::::::::::: callout

### What's assert?

Assertions are the simplest type of test. They are used as a tool for bounding acceptable behavior during runtime. The assert keyword in python has the following behavior:

```python
assert 1==1  # passes
assert 1==2  # throws error:
```

```output
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError
```

That is, assertions raise an `AssertionError` if the comparison is false. It does nothing at all if the comparison is true. Assertions are therefore a simple way of writing tests.

```python
assert mean([1,2,3]) == 2
```

::::::::::::::::::::::::::::::::::::::::::::::::

Activate your conda environment:

```bash
conda activate goodpractices
```

Check the version of `pytest`:

```bash
pytest --version
```

Finally, run the test:

```output
pytest example.py
======================== test session starts ========================
platform linux -- Python 3.6.9, pytest-7.0.1, pluggy-1.0.0
rootdir: /home/ole/Desktop/pytest-texample
collected 1 item
 
example.py .                                                  [100%]
 
========================= 1 passed in 0.00s =========================

```

When `pytest` is run, it will search all directories below where it was called, find all of the Python files in these directories whose names start or end with `test`, import them, and run all of the functions and classes whose names start with `test` or `Test`. This automatic registration of test code saves tons of human time and allows us to focus on what is important: writing more tests.

When you run `pytest`, it will print a dot (`.`) on the screen for every test that passes, an `F` for every test that fails or where there was an unexpected error. The tests pass when they do not throw errors. In rarer situations you may also see an `s` indicating a skipped tests (because the test is not applicable on your system) or a `x` for a known failure (because the developers fixed the problem shown in the test). After the dots, pytest will print summary information.

::::::::::::::::::::::::::::::::::::: callout

### Tests collection

If you do `pytest dir`, the `pytest` package ‘sniffs-out’ the tests in the directory and ran them together to produce a report of the sum of the files and functions matching the regular expression `[Tt]est[-_]*`.

::::::::::::::::::::::::::::::::::::::::::::::::

What happens if we break the test on purpose?

```python
def add(a, b):
    return a - b  # Uh oh, mistake! 😱
 
 
def test_add():
    assert add(2, 3) == 5
    assert add('space', 'ship') == 'spaceship'
```

Let's save the edits and run `pytest` again:

```output
======================== test session starts =========================
platform linux -- Python 3.6.9, pytest-7.0.1, pluggy-1.0.0
rootdir: /home/ole/Desktop/pytest-texample
collected 1 item
 
example.py F                                                   [100%]
 
============================== FAILURES ==============================
______________________________ test_add ______________________________
 
    def test_add():
>       assert add(2, 3) == 5
E       assert -1 == 5
E        +  where -1 = add(2, 3)
 
example.py:6: AssertionError
```

You can notice that functions fail on the first error, but **all test functions are executed**.

::::::::::::::::::::::::::::::::::::: callout

### Pure vs impure functions

**Pure functions** are deterministic, have a return value, have no side effects[1], and have referential transparency[2]. Thus, pure functions are easy to understand and test.

[1] Side effects: interactions of a function with its surroundings.
[2] Replacing a function call with the return of that function should not change anything.

Examples of pure functions:

```python
def last(my_array):
    return my_array[-1]
 
def add(a, b):
    return a + b
```

On the other hand, impure functions can be both intuitive:

```python
my_list = []
 
def append_to_my_list(item):
    my_list.append(item)
 
 
def read_data(file_name):
    return pd.read_csv(file_name)
 
 
def get_random_number(number):
    return random.random()
```

And not so intuitive:

```python
def hello(name):
    print("Hello", name)
 
 
nums = [1, 2]
 
def append(a_list, item):
    a_list += [item]
    return a_list
 
print(nums)            # [1, 2]
print(append(nums, 3)) # [1, 2, 3]
print(nums)            # [1, 2, 3] 😬
```

Some side effects can be indeed necessary or hard to spot.

Use pure functions when possible 👌

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Test-Driven Development: FizzBuzz Function (15 min)

The function `fizz_buzz()` takes an integer argument and returns it, BUT:

- Fails on zero or negative numbers.
- Instead returns "Fizz" on multiples of 3.
- Instead returns "Buzz" on multiples of 5.
- Instead returns "FizzBuzz" on multiples of 3 and 5.

Create an empty function `fizz_buzz()` and go through the conditions listed above, one by one:

1. Write a test for the condition.
2. Edit the `fizz_buzz()` function until the test passes.

Then discuss together the different solutions.

:::::::::::::::::::::::: solution 

## Solution
 
Add here the preferred solution. We don't have a ready one. 

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Tests are meant for preserving functionality by detecting new errors early and facilitating reproducibility for research software.
- Tests can help users in verifying correct installation and improving correctness for research output.
- Tests enable developers to make refactoring easier and simplify external contributions.
- Test-Driven Development (TDD) is an optional tool in your toolbox.

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
