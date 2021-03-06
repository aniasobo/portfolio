# Week one 28.05-2.06.2019

## Goals
- [x] Test drive a simple program using objects and methods.
- [x] Pair using the driver-navigator style.
- [x] Follow an effective debugging process.
- [x] Describe some basic principles like encapsulation, SRP.

## Challenges

- [x] Boris Bikes - Afternoons - Pair coding
- [x] Airport - Weekend - Individual

## Workshops
- [x] Intro to debugging
- [x] TDD

### Practice
- [x] Encapsulation and SRP practical
- [x] Debugging practical

-------------
# Raw notes below

## Debugging workshop

**Types of bug**

- syntax error
- gem/dependency not installed
- method/no method error/name error (trying to call an undefined/uninitialised object)
- incorrect logic when using/testing the program
- name/type errors

**Debug process**

1. Reproduce the bug
2. Read the error message(s)
3. Refer to the spec/user story/user need to identify what code is expected to do 
4. Print everything to tighten the loop/look into the steps of the program (p/print/puts); print around the line causing the problem; print a marker string around/before the problem line (for name errors); print numbered strings for step-by-step printing of problem lines

#### To do:
- [ ] debug the diary/appointment app
- [x] learn about scope

## TDD workshop

### Learning objectives

- [x] Explain why we do TDD
- [x] Describe/diagram TDD as a set of steps
- [x] Apply TDD following the diagram

**Notes**

- write test that mocks a bug (not a typo but a behaviour bug) & add to test suite
- mock: adds a state (initialises the buggy class in its buggy state & all its instance variables) to the instance under test
- Arrange, Act, Assert -- the 3 As of testing?
- passing values to methods as arguments (rather than hard-coding) makes the methods more flexible & testable
- test description - clarity = other coders can use the tests as spec/manual of expected behaviour
- breaking down logic/behaviour into tests helps understand the program
- start with simplest test & write the simplest code to make it pass (to avoid overcomplicating the code)
- tests = security when adding new code to legacy code
- write test - fail it. if it passes then it's useless (Red, Green, Refactor = write a failing test, make it pass, improve the code - both test and actual code - without changing behaviour)
- Gemfile - add gem to improve Rspec error editing
- write code & tests one at a time to avoid overengineering the program too early
- test should be checking behaviour - if behaviour tests pass, the test that checks the state (for ex., whether or not an object responds to the method) becomes obsolete and can be deleted


**Refactoring**
 
 - DRY - remove duplicates
 - rename variables
 - readability
 - length, if readability not scarified
 - speed/processing


**Arrange, Act, Assert**

Arrangement of class instances that can access requisite methods:

```
describe FileSystem do
	it 'can add items to storage' do
	filesystem = FileSystem.new #interchangeable with subject
	file = File.new
	filesystem.store(file)
	expect(filesystem.display_files).to include(file)
	end
end
```

Action - calling methods to test behaviour

Assert - the expect statement
	
### To do:

- [x] find out how to test randomness in Rspec 



