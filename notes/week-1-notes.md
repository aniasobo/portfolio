# Week one 28-31.05.2019

## Goals
- [ ] Test drive a simple program using objects and methods.
- [ ] Pair using the driver-navigator style.
- [ ] Follow an effective debugging process.
- [ ] Describe some basic principles like encapsulation, SRP.

## Challenges

- [ ] Boris Bikes - Afternoons - Pair coding
- [ ] Airport - Weekend - Individual

## Workshops
- [x] Intro to debugging

-------------
# Raw notes below

## Debugging workshop

**Types of bug**

- syntax error
- gem not installed
- method/no method error/name error (trying to call an undefined/uninitialised object)
- incorrect logic when using/testing the program
- name errors

**Debug process**

1. Reproduce the bug
2. Read the error message(s)
3. Refer to the spec/user story/user need to identify what code is expected to do 
4. Print everything to tighten the loop/look into the steps of the program (p/print/puts); print around the line causing the problem; print a marker string around/before the problem line (for name errors); print numbered strings for step-by-step printing of problem lines

#### To do:
- [ ] debug the diary/appointment app
- [ ] learn about scope

----------

## Boris bikes challenge 

_pairing: Anna & Rachel_

## Goals:

- I grow collaboratively
- I can model anything
- I can TDD anything

## Challenges

- [x] Setting up a Project
- [x] Working with User Stories
- [x] From a Domain Model to a Feature Test
- [x] Errors are good
- [x] From Feature Tests to Unit Tests
- [x] Passing your first Unit Test
- [x] Back to the feature
- [x] Back to the unit
- [x] Building a bike
- [x] Making Docking Stations get Bikes
- [ ] Using Instance Variables
- [ ] Raising Exceptions
- [ ] Limiting Capacity
- [ ] Using Complex Attributes
- [ ] The Single Responsibility Principle
- [ ] Removing Magic Numbers
- [ ] Initialization Defaults
- [ ] Dealing with Broken Bikes
- [ ] Isolating Tests with Doubles
- [ ] Mocking Behaviour on Doubles
- [ ] Men with Ven
- [ ] Modules as Mixins


### Things we learned:
- GitHub collaboration with both collaborators committing changes (driver initialised & added remote, navigator updates the tracking note & process notes)
- structure of user story
- stack trace -> list of method calls that the program was in the middle of when an Exception was thrown
- initialising the object in irb, as a nil object, solves the uninitialised constant error
- initialising rspec - added lib directory manually, added the first test file in the spec directory, ran rspec to confirm all is green/setup was successful 
- Rspec - use the 'subject' keyword to test instances of class (describe block contains class/object name which is the subject, similar to self)
- single-line Rspec syntax
