# Week three 10-16.06.2019

## Goals:

- [x] Build a simple web app
- [x] Follow an effective debugging process for web applications
- [x] Explain the basics of how the web works (e.g. request/response, HTTP, HTML, CSS)
- [x] Explain the MVC pattern

---  

## Practice:

Date | Project | progress
--- | --- | ---
10.06 | [Battle](https://github.com/aniasobo/poki-battle) - pairing | mostly completed
12.06 | Degugging workshop practical | completed
12.06 | [RESTful APIs practical](https://github.com/sjmog/rest) | completed
15-16.06 | RPS game | [work in progress](https://github.com/aniasobo/rps-challenge) | [review](https://github.com/makersacademy/rps-challenge/pull/1329/files)

---

## Lesson from weeks 1-3:

> Even if you have no time to finish a challenge, read all the remaining steps + their walkthroughs at the end, and watch a video walkthrough where available - you still learn some extra lessons that you can later apply in practice


### Notes on the weekend challenge/code review:

The correct way to stub the Twilio calling method:

```
describe Takeaway
  subject(:takeaway) { described_class.new }

  before do
    allow(takeaway).to receive(:send_text)
  end

  it 'sends a payment confirmation text message' do
    expect(takeaway).to receive(:send_text).with("Thank you for your order: £20.93")
    takeaway.complete_order(20.93)
  end
end
```

[other options:](https://github.com/makersacademy/course/blob/master/pills/levels_of_stubbing.md)

1. Stub Class in Your Application (code above)
2. Stub the Gem Associated with 3rd Party API
3. Stub the Network with Webmock
4. Manage Your Network Stubbing with VCR

---

### Code review workshop notes:

- private methods are not to be tested!
- be careful to not expose instance vars by assigning them as attribute accessors instead of readers
- `dotenv` gem: create `.env` files for your environment variables (as alternative to storing them in `bash_profile`), remember to add all `.env` files to `.gitignore`
- zsh? alt to Terminal
- integration test vs feature test - the former is concerned primarily with testing the relationships between objects/classes, the latter tests those naturally in the course of testing the app


### The two schools of TDD

[London school vs Chicago school of TDD](http://programmers.stackexchange.com/questions/123627/what-are-the-london-and-chicago-schools-of-tdd)

```
# London Style
describe Order do
  let(:menu) { double :menu, price: '£1.00', contains?: true }
  subject(:order) { described_class.new(menu) }

  it 'order total to be sum of items added' do
    order.add('Pizza')
    order.add('Pizza')
    expect(order.total).to eq '£2.00'
  end
end
```

```
# Chicago Style --> arguably an 'integration' or 'feature' test
describe Order do
  subject(:order) { described_class.new(Menu.new) } # note real Menu class

  it 'order total to be sum of items added' do
    order.add('Pizza')
    order.add('Pizza')
    expect(order.total).to eq '£2.00'
  end
end
```

---

## Debugging web apps workshop:

> "Tighten the loop; Get visibility."

- find the exact line with the bug; to tighten the loop: use p to get visibility; read the stack trace

**STEPS**

1. Take a break
2. Rubber duck
3. Check your assumptions
4. Follow the flow and get visibility
5. Repeat

**types of bugs:**

1. Error in code - syntax error, name error etc
2. Unexpected behaviour - expected vs actual (code works but doesn't do what you want it to)

**save_and_open_page**

- for debugging with Capybara (a Capybara method)
- takes a snapshot of the page

#### process:

1. added `require shotgun` to `app.rb` to make it run in localhost
2. changed struggle word across code 
3. added another emoji to the happy emoji sample array
4. model - view - controller pattern: `app.rb` is the controller; `struggle_table_flipper.rb` & `random_happy_emoji.rb` are the models; controller sends & receives messages from/to model; `index` & `flipped_struggle` are views; no interaction between model and view; what view returns will be displayed to the user by the controller

---

## RESTful APIs:

REST - a set of conventions for writing routes

### Resources

Web = network of resources; resource = data stored somewhere  

**a resource is a "//noun// stored //location//"**

### Representations  

Representation = route for a user to take to a resource (ex. stuff that ties the URL to an action)

**NOUN/plural/id**  

Example RESTful representations:

```
GET /bookmarks/1
GET /users/217
GET /image.jpg
GET /bookmarks/1
GET /index.html
```

**Web applications are state machines and REST defines their interface**

RESTful routing exposes the nature of your web app - a state machine capable of a certain variety of states.  

Movements between those states are determined by user interactions, called **state transitions**:  

state | state transition | RESTful route  
--- | --- | ---
Having 35 bookmarks | returns 35 bookmarks | GET /bookmarks
Adding a bookmark | transitions the machine to a new state, returns 36 bookmarks | POST /bookmarks
Deleting a bookmark | transitions the machine to a new state of 35 bookmarks, returns 35 bookmarks | DELETE /bookmarks/4

#### states & state transitions:

- Having 35 bookmarks (state)
- Adding a bookmark (state transition)
- Having 36 bookmarks (state)
- Deleting a bookmark (state transition)
- Having 35 bookmarks (state)


### Ruby Net class

a library for building http user-agents


```
require 'net/http'
```

get web content as string:

```
Net::HTTP.get('example.com', '/index.html') # => String
```

get web content by URI (it's automatically required with Net so no need to additionally require it:

```
uri = URI('http://example.com/index.html?count=10')
Net::HTTP.get(uri) # => String
```
---

## OOP

> Good OOP is about telling objects what you want done, not querying an object and acting on its behalf. Data and operations that depend on that data belong in the same object.

> [Tell, don’t ask!](https://thoughtbot.com/blog/tell-dont-ask)

[How to write good classes.](https://thoughtbot.com/blog/meditations-on-a-class-method)

## Metaprogramming 

Problem: the `@instancevar` goes out of scope when response is sent.  

**Solution:**  

- call methods on the class itself, as opposed to instance (like `.new`)
- do this by prefixing the method name with `self`.

```
class MyClass
  def self.my_class_method(some_arg)
    # to call this method you would do this:
    # MyClass.my_class_method('an argument')
    @arg = some_arg
  end
end
```  

- `@arg` is NOT visible to any instance of `MyClass`; it's only accessible to other class methods (so other `self.methods`)
- to call the above method:

```
MyClass.my_class_method('an argument')
```

- in Battle challenge:

```
def self.create(player1, player2)
  @game = Game.new(player1, player2)
end

def self.instance
  @game
end

#called like this:

@game = Game.instance
```

- both create and instance have access to `@game`
- in the controller, run those like this:

```
post '/playernames' do
  player1 = Player.new(params[:player1name])
  player2 = Player.new(params[:player2name])
  @game = Game.create(player1, player2)
  redirect '/battle'
end

get '/battle' do
  @game = Game.instance
end
```

- then refactor with a Sinatra filter:

```
before do
  @game = Game.instance
end
```

- this way `@game` is defined in every route, and in `/playernames` it gets overriden by `@game = Game.create(player1, player2)`

---  

## Empathy workshop

_importance of empathy_  

The main domains of EI: self awareness, self regulation, empathy, social skills, motivation.  

_common hindrances_

_ways to train empathy_

1. everyone is just like me
2. loving-kindness meditation (Metta Bhavana)
3. empathetic listening (pretend you'll have to write a test on what the other person is saying later)

