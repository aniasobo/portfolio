# Airport challenge

## Approach:

- drew out the logic based on user stories
- identified nouns and verbs to inform IA
- set up test files for my class files

---

## Logic:

The program is divided into 3 classes: Airport, Plane and WeatherReport. 

**Airport object:**   
- can be assigned custom capacity when initialized
- is initialized in an empty state
- calls ground control to return current number of planes
- receives requests from planes: to land and to take off
- has private methods that act as tower: they ask another private method for current weather report before issuing permission or denying it to the methods that receive requests from planes 

**Plane object:**
- is assigned status of "in air" by default (as Airport objects are initialised in an empty state)
- can be assigned status "grounded" with the .update method

**WeatherReport object:**
- randomly selects weather forecast from an array of forecasts, 7 of which are good for flight and 3 of which are "stormy"

---

## User stories covered:

As an air traffic controller    
So I can get passengers to a destination  
I want to instruct a plane to land at an airport  

As an air traffic controller    
So I can get passengers on the way to their destination  
I want to instruct a plane to take off from an airport and    confirm that it is no longer in the airport    

As an air traffic controller     
To ensure safety    
I want to prevent takeoff when weather is stormy    

As an air traffic controller  
To ensure safety  
I want to prevent landing when weather is stormy  

As an air traffic controller     
To ensure safety     
I want to prevent landing when the airport is full    

As the system designer    
So that the software can be used for many different airports    
I would like a default airport capacity that can be overridden  
as appropriate    

---

## Concepts learned:

- Rspec mocking
- practical TDD 

---
 
### To do: 

- tests are not DRY and should be refactored
- suspected edge cases that will fail program: plane already grounded can land, plane already in air can take off
- suspected incorrect test syntax in mocking methods
- feature testing to add

---

## Notes from comparison with model solution:

[Link to model solution](https://github.com/makersacademy/airport_challenge/pull/1238/files)  

- method for parking planes should update the plane status first, then park it 
- methods for parking and releasing planes should handle errors instead of returning a string when failed

```
  def land(plane)
		raise 'Airport full' if full?
		raise 'Bad weather' if stormy?
		plane.land
	
		@planes << plane
  end
```

- simpler way to write the weather class (returns true if over 4, ie stormy):

```
class Weather
  def stormy?
		Kernel.rand(0..6) > 4
  end
end
```

- it was a good decision to make planes in flight by default
- good practice to keep the user stories in the spec file as comments directly preceding the tests that cover them
- setting up an it block correctly with a mocked weather:

```
	weather = Weather.new
	allow(weather).to receive(:stormy?).and_return(false)
```

- top describe block should start like:

```
RSpec.describe Plane do
end
```

- 