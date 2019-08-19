# Week two 3-9.06.2019

## Goals:

- [x] I write code that is easy to change  
- [x] I can test-drive my code  
- [x] I can build with objects  

---  

### Code reviews:

- helps you gain insight into different ways of coding same problem
- checking readability and maintainability
- knowledge sharing
- learn to read code
- ensuring consistency of codebase (at a company)
- only reviewed & approved code can be pushed to production

#### Code review how to:
- go to the pull request in the Makers challenge repo
- find your pair's pull request
- go to Conversation - this could include comments from the pull requester 
- go to Files changed
- code in green is added - click + to the left of the line you want to comment about
- top right corner - green button Finish your review (opens a longer comment input form)
- use the Code review rubric to see what feedback should be about
- it's ok to ask questions & add code suggestions in the comment

1. start with the `README`
2. check spec files to make sure they cover all user stories
3. check readability and DRYness of the code - mark unclear parts
4. suggest refactoring if it could make something shorter while staying readable
5. review commit by commit but it's ok to keep the comments for the final version

### Conventions:

- use of camel case for class names, snake case for variables
- important to stick to because your code gets reviewed by others and sticking to conventions makes it more readable/reduces fatigue
- use a linter (rubocop) before submitting 

#### Predicate methods

- predicate methods are methods that return a boolean
- they should end with `?`
- they should be private?
- if extended, should only return truthy values
- to ensure they only return booleans, use double negative like so: `!!@is_true?` (in practice: `@is_true?` will return `nil`, `!!@is_true?` will return `false`)
- ["One of the maxims of good programming is to "be liberal in what you accept and strict in what you emit". Returning a boolean from predicate methods is being strict in what you emit."](http://pragmati.st/2012/03/24/the-elements-of-ruby-style-predicate-methods/)

#### READMEs  

- good place to start reviewing the code
- could include diagrams, approach and/or goals
- could include test coverage and if the tests are passing or not
- [README how to](https://medium.com/@meakaakka/a-beginners-guide-to-writing-a-kickass-readme-7ac01da88ab3)
- [README pill](https://github.com/makersacademy/course/blob/master/pills/readmes.md)
- [README example](https://github.com/matiassingers/awesome-readme)  

---  

## Practice:

Date | Project | progress
--- | --- | ---
Mon 3.06 | [Oyster Card](https://github.com/aniasobo/oystercard1) with Aleks | 50% done
4-5.06 | TDD practice - [Birthdays Calendar](https://github.com/aniasobo/birthdaycal) | done, awaiting review
6.06 | Domain modelling workshop & practical | in progress
7.06 | [Testing OO relationships practical](https://github.com/aniasobo/testing-relationships-between-classes) | in progress
8-9.06 | [Takeaway](https://github.com/aniasobo/takeaway-challenge) - weekend challenge | [review notes](https://github.com/makersacademy/takeaway-challenge/pull/1351)

---

## Domain modelling workshop:  

1. read requirements/user stories
2. mental walkthrough
3. extract nouns & verbs
4. diagram objects & messages
5. feature test - use user stories as comment blocks before each test
6. unit test (first user story) 
7. fail both
8. make them pass
9. refactor
10. repeat

**UML**

- [Unified Modeling Language](https://www.ibm.com/developerworks/rational/library/769.html)

### User stories:

classes: Note & Notebook
- [x] Note - initialised with a tag attribute (empty)
- [x] Notebook - initialised with an empty container (hash?) for tagged notes and an empty container for untagged notes
- [x] `Notebook.add(note)` -> if note has an argument, `Note.tagged(tag)` -> added to Notebook as `{ :tag => note }` if no argument -> add to `Notebook` array
- [x] `Notebook.find(tag)` -> returns values with key `:tag` (without argument returns the array of untagged notes)
- [x] Note -> `.add` checks if note is text only, raises error if not

---

## Rspec mocking workshop 7.06

- mocks are for classes (to test class in isolation)
- use doubles when you don't want the code of a particular method to run
- use instances inside it blocks to start with initial state for each test (isolation again)
- let method (like the `before` method) makes the code DRY because it runs the same statements before each it block
- store objects as early as possible to have access to full set of their methods later
- mocks can be created as classes on top of the spec file
- mock = `double('text', bye: 'more text')` => names the double, gives it a method and something to return; same as: `allow(mock).to receive(:bye).and_return('more text')`
- use instances in the feature test
- doubles don't care about additional, unspecified args

#### Correct order:

1. setup each test in isolation
2. execute
3. verify
4. tear down (happens automatically)

#### pry gem:

- add to gem file, bundle etc
- it's like irb for the spec
- add `binding.pry` to spec file inside the it block where you want to pick up (stuff before will be executed like in irb with require but without the full file)
- add the require in the `spec_helper` - `require 'pry'`
- `rspec -fd` (?? opens pry?)
- `.rspec` autogenerated file has the `require "spec_helper"` so you don't have to require it in your spec files (unless you don't have it in your project)