# Week two 3-9.06.2019

## Goals:

- [ ] I write code that is easy to change  
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

1. start with the README
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
- they should end with ?
- they should be private?
- if extended, should only return truthy values
- to ensure they only return booleans, use double negative like so: !!@is_true? (in practice: @is_true? will return nil, !!@is_true? will return false)
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

classes: Note & Notebook
- [x] Note - initialised with a tag attribute (empty)
- [x] Notebook - initialised with an empty container (hash?) for tagged notes and an empty container for untagged notes
- [x] Notebook.add(note) -> if note has an argument, Note.tagged(tag) -> added to Notebook as { :tag => note } if no argument -> add to Notebook array
- [x] Notebook.find(tag) -> returns values with key :tag (without argument returns the array of untagged notes)
- [x] Note -> .add checks if note is text only, raises error if not