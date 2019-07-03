# MakersBnB

_team:_ 

Carl, Chris, Remzilla

_stand ups_ 10:30  
_retros_ 17:00  


## Development workflow

- [ ] Turn the spec into user stories.
- [ ] Create one GitHub issue for each user story.
- [ ] Pick the most important user story and follow this development workflow.
- [ ] Return to step 3.


## Project setup  

- [x] One member in your group, create a GitHub repo for your Makersbnb project.
- [x] Add the other members of your group as collaborators.
- [x] Person who adds pull request merges after feedback from team

## TECH STACK:

- Sinatra app 
- PostGres db  
- JS/JQuery interface
- CSS styles
- hosted on Heroku


### Add a README that has:

- [ ] A description of the high level description of the spec.
- [ ] A user stories section.
- [ ] Start turning the specification into user stories.
- [ ] Create a branch.
- [ ] Add the user stories to the README.
- [ ] Use the developer workflow to get the README merged into master.

### Misc to do:

- [x] team slack channel
- [x] agree on standup/retro routine
- [x] plan work with kanban
- [ ] set up a CI
- [x] GitHub repo


### Merge process:

1. Make sure your local master is up to date - 'git pull' before working every time
2. Create a local branch, once it passes tests locally... 'git checkout -b [name_of_your_new_branch]'  
3. Make sure you're on the right branch ' git branch -a'
4. add a new remote to branch 'git remote add [name_of_your_remote] name_of_your_new_branch'
3. ...push your branch to GitHub 'git push origin [name_of_your_new_branch]'  
4. Create a pull request from your master to master-master??
5. remember to switch back to master and delete branch
5. CI runs on master
6. deploy to Heroku from master

--[instructions](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches) --

## Backend:

dbname: makersbnb
test db: makersbnb_test

tables: users, spaces

to do:

- [ ] test database helper - method that runs before each Rspec test and clears the test database
- [x] add to README: create both databases (after bundle)


## Database on Heroku:

- add Postgres plugin to heroku 
- get database details (name, host, port, username, password) from heroku dashboard, [add in db connection]((https://www.rubydoc.info/gems/pg/PG%2FConnection:initialize)) like so:

```
PG::Connection.new("ec2-50-16-197-244.compute-1.amazonaws.com", 5432, nil, nil, "d37k5fffpt81gq", "mwtacjgvugnztj", "53332d96369b96d480139e1fd78566a94eb886172ed0ce26bab98bba31067a57")
```

## Debugging routes in controller:

- does the route start with a '/'?
- 

## Resources:

[Specifications](https://github.com/makersacademy/course/blob/master/makersbnb/specification_and_mockups.md)  
[Mock-ups](https://github.com/makersacademy/course/blob/master/makersbnb/makers_bnb_images/MakersBnB_mockups.pdf)  
[Course guidance](https://github.com/makersacademy/course/tree/master/makersbnb#development-workflow)  
[PG Connect](https://www.rubydoc.info/gems/pg/PG%2FConnection:initialize)