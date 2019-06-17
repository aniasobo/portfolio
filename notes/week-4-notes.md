# Week four 17-23.06.2019

## Goals:

- [ ] Build a simple web app with a database
- [ ] Follow an effective debugging process for database applications
- [ ] Explain the basics of how databases work (e.g. tables, SQL, basic relationships)

---  

## Practice

Date | Project | progress
--- | --- | ---


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

## Databases:

- Model interacts with the db; one model per table (usually) - model becomes a collection that manages the data