# Chitter challenge

## Approach

### 1. Research and planning

I decided to use DataMapper to model my database relations.

DataMapper resources used:  
- official documentation 
- [this video tutorial](https://www.youtube.com/watch?v=G93-ZVw_S2c)

I decide not to worry too much about security of my users because implementing registration is a new thing for me so I start with the basics

**CRCs:**

_User_  
| Responsibilities | Collaborators | 
| --- | --- |   
| has id | ? |   
| has a name | ? |   


_Peep_  
| Responsibilities | Collaborators |   
| --- | --- |   
| has id | ? |  
| author | User |   
| has text | ? |  
| timestamp | ? |   




### 2. Setup

- added data mapper gems, pg, sinatra etc, ran bundle
- checklist for setting up Ruby projects completed
- added a test_db helper for spec_helper
- added a db.rb with data mapper setup and my CRC models in README - first commit ready
- testing db.rb locally: ugh 
- many failed attempts later, I use [this repo](https://github.com/Rosa-Fox/todo-sinatra-datamapper) and [this resource](http://cheat.errtheblog.com/s/datamapper) to refactor my setup
- I'm not sure how to test my setup as it's all new and I've made many guesses as to what does what
- I make an executive decision not to use TDD for this because it adds another level of difficulty to an already complicated virgin use of this tool
- added basic views, on to feature tests
- feature tests pass, on to my models
- added all basic functionality but low test coverage, to be added later


### To dos:

- [ ] guessing that I don't actually need the pg gem at all? refactor
- [x] refactor db.rb to extract classes
- [ ] use the database cleaner gem?
- [ ] no idea if I'd set up the test database correctly - how to test? find out
- [ ] refactor app.rb to move classes to lib files
- [ ] add unit tests for the above