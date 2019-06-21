# Daily Diary 

Daily Diary is an application to store daily diary entries, using Sinatra and PostgreSQL.

### To dos:

- [ ] I'll create a working implementation of the system described above (empirical)
- [ ] I'll be able to diagram the flow of information through my application, from user interactions through to the database (empirical)
- [ ] I'll share my diagram with a coach in order to receive feedback (credible)
- [ ] refactor db connection to be its own class, take the if statements out of the Entry class
- [ ] add automatically added timestamp that gets returned and displayed on the list


## Functionality:

- [x] Add diary entry
- [x] Save entry with a title 
- [ ] save entry with a timestamp
- [ ] view list of entries by title
- [ ] click on title to view full entry
- [ ] edit saved entry
- [ ] delete entry
- [ ] add comment to entry
- [ ] display comments when entry is viewed
- [ ] add tag to entry
- [ ] filter entries by tag


**README to dos**  

- [x] instructions for setting up the databases, including table setup steps.
- [ ] instructions for how to run tests
- [ ] instructions for running the application
- [ ] overview of your approach and design


### Processes used:

- TDD
- modelling
- self-directed learning
- diagraming
- coding!
- problem solving/debugging


### Approach:

- as first step, I set up the project with rspec, capybara and sinatra, following the ruby project setup checklist
- I added the user stories I'm planning to cover to feature test spec files
- starting with a single database to make sure functionality is QA'ed before adding a test database
- I write feature test first because BDD; starting with adding entries to diary app
- to make the feature test pass, I add the view with the form to '/'
- added an initialise method to Entry class that is called as the return statement of the class methods, so that instances of Entry can be passed on to objects when those methods are called
- added Rack::MethodOverride in order to use RESTful routes
- I couldn't get the DatabaseConnection class to talk to the Entry class so I added the db connection logic to Entry for now so that I could keep building the functionality of my project 
- I added a success view to give the user feedback about a successfully saved diary entry
- next step: adding a list of clickable titles. I add a feature test for this; I'm testing using a PUT route for this, so to make things easier I refactor the entries view to be a form with action put that will pass on the ID of the chosen entry (hoping to refactor this later back into links)
- refactored my app to have a list of options in index; the add entry form, previously in the index view, is moved to its own view: new