# Week four 17-23.06.2019

## Goals:

- [x] Build a simple web app with a database
- [x] Follow an effective debugging process for database applications
- [x] Explain the basics of how databases work (e.g. tables, SQL, basic relationships)

---  

## Practice

Date | Project | progress
--- | --- | ---
17.06 | [Bookmark manager](https://github.com/aniasobo/bookmark-challenge) | [pairing with Rhys](https://github.com/aniasobo/portfolio/blob/master/feedback/feedback%20from%20Rhys.md); [progress note](https://github.com/aniasobo/portfolio/blob/master/challenges/bookmark-manager.md)
19-22.06 | [Daily Diary app](https://github.com/aniasobo/daily-diary-app) | [progress note](https://github.com/aniasobo/portfolio/blob/master/challenges/daily-diary.md) 
20.06 | working on [Remy's Bookmark manager repo](https://github.com/IndecentDolphin/bookmark_manager/) | step #13 completed
22-23.06 | [Chitter challenge](https://github.com/aniasobo/chitter-challenge) - [notes](https://github.com/aniasobo/portfolio/blob/master/challenges/chitter.md) | weekend project - basic completion

---  

## Code review for RPS  

- no need to test all game logic in unit tests - only all outcomes in feature test
- Randomiser class uses rand(0..2) method, srand(x) in test controls randomness; alt solution: stub out rand:

```
# in class method
Kernel.rand(0..2)

# in test
allow(Kernel).to receive(:rand)
```

- Kernel: a Ruby module; all its methods can be used on any Ruby object (visible in irb with Kernel.methods) because all objects inherit from Kernel
- separate logic from presentation - no strings in the controller and models, only in views; views can have logic that displays string depending on the outcome/value of var/sym (but avoid using instance variables/having excess logic)
- class Weapon for handling moves - makes game extendable

```
class Weapon
	def initialize(name, beats)
	end 
end
# relies on a constant with weapons living somewhere in the game
```

- sessions: hash stored in browser; ok for user id, not ok for storing entire game logic
- singleton pattern (alt to using sessions and global vars): uses class methods (self.)

```
def self.create(player1, player2)
@game?
return @game
else
@game = Game.new(player1, player2)
end
# checks if there's already a game running, sets instance to that currently running game
```

- use db over singleton pattern

---

## Misc tips and tricks:

**[Removing DS_Store from a GitHub repo via .gitignore](https://stackoverflow.com/questions/107701/how-can-i-remove-ds-store-files-from-a-git-repository)**

magic line:

```
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

run the above in terminal, then add .DS_Store to .gitignore & commit

[alternative way to do this](http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/)


**Fix for killing postgres process that blocks the port**

(a.k.a. FATAL database does not exist - because postgres can't look into its default 5432 port due to old processes running)

```
brew services stop postgresql
```

using kill process functions (saved in bash_profile) and killing processes by PID in Activity Monitor or Terminal will not help, because Postgres process immediately respawns its children.  

---

## ERB views

<% %>s without the = get executed but not displayed in the view

Displaying all bookmarks in the bookmarks array in index:

```
<h1>Bookmark Manager</h1>
<ol><% @bookmarks.each do |bookmark| %>
<li><a href="<%= p bookmark %>"><%= p bookmark %></a></li>
<% end %>
</ol>
```

[Intro resource](https://www.stuartellis.name/articles/erb/)


---

## Uncovering database design workshop

- modelling a domain with Class Responsibility Collaborator cards
- one-to-many relationship should exist on the many (on Bikes as opposed to on Docking Stations)
- many-to-many - joined table
- each table should be associated with a class
- joined table doesn't require an id
- joined table is associated with a class - querying the table creates instances of it (self method?)
- use class methods to query the db associated with a class (not instance method)
- never put lists in a table cell - if this is required, it means you need to redesign the table into more than one table

**goals**

- [x] Explain how to use CRC cards to model a domain
- [x] Model a simple domain using CRC cards
- [x] Infer database structure from domain structure

- Model interacts with the db; one model per table (usually) - model becomes a collection that manages the data
- [This resource](https://guides.rubyonrails.org/association_basics.html#the-types-of-associations) has good info on associations between tables


#### CRC:

_Class_  

| Responsibilities | Collaborators | 
| --- | --- | 
| action | agent |

**Examples:**  

_DockingStation_  

| Responsibilities | Collaborators | 
| --- | --- | 
| release_bike | Bike |
| dock | Bike |
| bike_count | Bike |


_Bike_  

| Responsibilities | Collaborators | 
| --- | --- | 
| working? | Bike |  

**Designing db structures:**

_Table: bikes_  

| id | working | docking_station_id |
| --- | --- | --- |
| 1 | true | 1 |


_Table: docking_stations_  

| id | 
| --- | 
| 1 | 


## RESTful routes in Sinatra

Extracted from [this README](https://learn.co/lessons/sinatra-restful-routes-readme)

For the initialize class, [refer to this](https://itnext.io/removing-argument-order-dependencies-c5e2482ba208)

---

## Retro 21.06.2019

- don't be stuck - ask a coach (practice for being a junior in a dev team)