# Week 10, 29.07-04.08.2019

## Goals: 

- [x] master the tech test process


## Practice

Date | Project | progress
--- | --- | ---
29-31.07 | [Bank](https://github.com/aniasobo/tech-test-bank) | individual work
1.08 | Gilded Rose - Ruby - JS | individual work - in progress


---

## Tech test

### Documentation - README

- installation instructions
- how to run tests
- user stories/acceptance criteria
- overview of what the program does
- your approach

### Requirements

- what are the acceptance criteria 
- expected input/output (output to where?)
- plan not to stray from the requirements

### Code quality

- DRY
- SRP
- Readable: naming conventions, linting, clear syntax, line length etc
- applies to both tests and code
- SOLID acronym
- use git!


## Tech test checklist

**Don't submit a tech test without running through these questions first**.

If any of the questions are unclear, take a look at out our guide for [improving your code](improving_your_code.md)

- [x] Is your code [properly tested](#testing-checklist)?

- [x] Does your repository have a [good README](#readme-checklist)?

- [x] Re-read the original task and check you've fulfilled all the requirements.

- [ ] Is your code formatted idiomatically?

- [x] Does your code look correctly formatted on GitHub as well as on your computer?

- [x] Have you taken as much logic as possible **out of your controllers** into models/libraries?

- [x] Have you taken logic **out of your views**?

- [x] Does your code follow the **Single Responsibility Principle**? Ask each class, spec and method/function what it does, if the reply involves the word "and" you probably need to refactor.

- [x] Are the units well encapsulated?

- [x] Have you kept your **methods/classes as small as possible**?

- [x] Have you run your code through a linter?

- [x] Do all your **names make sense**? Can someone else understand what's going on without you having to explain it to them? Do your names use the language of the problem domain?

- [x] Is any of your code doing anything **unusual/suprising**?

- [x] Have you removed all comments except those that are absolutely necessary?

### Testing checklist

- [x] Is all your code **tested** (especially unit tests but also feature tests where appropriate)?

- [x] Are your tests passing?

- [x] Do you have high test coverage?

- [ ] Have you tested unhappy paths and edge cases?

- [x] Do your unit tests mock their collaborators?

- [x] Do you always test for behaviour, rather than state?

- [x] Do your specs **read well** when you run them?

### README checklist

- [x] Describe how you approached designing your solution to the problem.

- [x] Describe how you structured your code.  Why did you do it this way?

- [x] Describe how to install and run your code and tests.

- [x] Describe the dependencies your code has.  What trade-offs did you make when deciding what dependencies to use?

- [x] If you've deployed the app, include a link to it.

- [x] Include screenshots of your running app.

- [x] Try very hard to complete all the tasks in the tech test.  If you run out of time, outline how you would have approached the sections you didn't get to.

- [x] Describe the extensions you would add if you had more time.

- [x] Spelling and grammar.

---

## Testing behaviour not state

- State: object's attributes
- initial state should not be tested
- using attribute reader for tests - not recommended, better to use an existing method that returns that value
- start with testing the method that other methods are dependent on for testing, and test it in isolation first
- don't add attribute readers only for tests' sake

---

## Tech CVs

GitHub CV - first thing the HPs see when applied too.

one-page cv: `enhancv.com`


### personal profile: 

- identity as software dev
- sell yourself, not Makers
- highlight relevant experience
- reason for career change
- what do you love about tech
- short paragraph length


### Projects:

- don't suggest level of proficiency in any tech - link to projects where tech was used instead, and list it
- the most important part of the cv
- pick the projects you're most proud of
- they don't have to be finished but they should have polished READMEs
- 3-5 max


### Skills section:

- pick the skills you want to talk about first
- specific examples to illustrate you can use those skills
- soft skills - think of how to prove/demonstrate


### Experience & education:

- relevance to tech
- explanation of longer gaps
- (mention learning languages, research skills in connection to degree)
- skip secondary education, keep the degree but make it relevant


### Hobbies, volunteering, meet-ups attended:

- don't skip
- be serious
- what you're learning right now
