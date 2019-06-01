# Boris bikes challenge 

_pairing: Anna & Rachel_
_pairing with: Monika_
_pairing with: Leon_

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
- [x] Using Instance Variables
- [x] Raising Exceptions
- [x] Limiting Capacity
- [x] Using Complex Attributes
- [x] The Single Responsibility Principle
- [x] Removing Magic Numbers
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


### Things we learned:

- attribute readers
- methods can return other objects/instances of other classes
- guard condition: using keyword 'fail' on first line of method, adding 'unless' later for proper method behaviour
- Rspec describe - hashtag methods within classes
- Rspec - nested describes
- Rspec syntax for expecting error
- rspec --backtrace shows full stack trace for error analysis.
- Single Responsibility Principle - a design principle, used in refactoring; each method to only do one thing
- using constants to replace magic numbers
- encapsulation = putting the literal into a constant to use everywhere else

**Private methods:** 
- don't have to be tested
- extract method responsibilities to other method, in adherence to the SRP 
- good object interface design requires the separation of public, protected and private methods
- important to the object's internal implementation but of no concern to the public
- can't be called

## SOLID:
- [x] S - Single Responsibility Principle
- [ ] O - Open/Closed Principle
- [ ] L - Liskov Substitution Principle
- [ ] I - Interface Segregation Principle
- [ ] D - Dependency Inversion Principle