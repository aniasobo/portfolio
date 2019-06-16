# Week 3 Intro to Web challenge

- localhost is your machine's host name for itself
- 4567 is the port used to connect to localhost
- localhost:4567 is where Sinatra is listening for connections
- default for websites is port 80, which is why it's never displayed in the request:

```
www.google.com:80
```

## httpie gem:

- a command line tool for making HTTP requests
- acts as a client, together with Terminal, so responses from requests are loaded to Terminal (for example, web content)
- set up:

```
brew install httpie
```

- view manual:

```
man http
```

and:

```
http --help
```

- to make a server request:

```
http server-url-here
```

- verbose mode request:

```
http -v server-url-here
```

- sending data to server:

```
http -f POST https://getpostworkout.herokuapp.com/ name=Ptolemy
```

### parts of the URL:

- "/home" is the path to the resource on the server (comes after the address)
- "?name=Bob&age=21" is a query string:
- ? begins the parameters after the path
- name=Bob is a parameter
- & separates parameters
- name and age are keys, Bob and 21 are values

## shotgun gem:

- restarts local server on every request (when code is edited & saved)
- no need to restart the local server to see changes applied on localhost
- add this to Gemfile of the project and bundle
- for sessions to work in development mode, set them to secret like so:
- run with Sinatra like this:

```
shotgun app.rb -p 4567
```

- the p tells shotgun which port to use
- shotgun uses port 9393 by default
- (substitute shotgun for ruby in that command to run without shotgun for debugging)
- to secure session data, add this to your app:

```
set :session_secret, 'super secret'
```

- in shotgun documentation, run this if server isn't rendering in localhost:

```
shotgun config.ru
```

### config.ru

[SOURCE](https://dev.to/morinoko/the-basics-of-sinatra--la-mvc--configuration--routes--forms-417e)

- required for Rack-based apps
- loads the environment of the app
- use & run keywords specify controllers 
- run starts the application server

```
require_relative './config/environment'
run ApplicationController
```

Above: the config/environment file loads the environment; the ApplicationController (application_controller.rb) is the only controller.

**config/environment.rb**

- gets the application code connected to all the gems
- loads bundler and all the model, view and controller files in the app directory

```
ENV['SINATRA_ENV'] ||= "development"
ENV['RACK_ENV'] ||= "development"

require 'bundler/setup'
Bundler.require(:default, ENV['SINATRA_ENV'])

require_all 'app'
```

(require_all is a gem and needs to be added to Gemfile and bundled)

**Application Controller**

- handles all incoming requests, responses and routing
- the app controller needs to create a class that inherits from the Sinatra base:

```
class ApplicationController < Sinatra::Base
end
```

- Sinatra base gives the app a Rack-compatible interface
- single controller for single apps - define all URLs and how they should respond to GET and POST requests 
- '/' is the root domain
- the params hash - contains attributes set by the URL parameters (input by the user)

```
get '/recipes/:id' do
  # The :id is passed through the URL,
  # which is accessible in the params hash.
  # Use it to assign a recipe to an instance variable
  @recipe = Recipe.find(params[:id])
  erb :'recipes/show'
end
```

**Passing data to views through instance variables**

- instance variable in a controller route = available in the corresponding view file (NOT available in other routes within the controller

**Models**

```
# models/recipe.rb

class Recipe
  attr_accessor :title, :description, :ingredients, :method
end
```

- once a recipe object has been assigned to @recipe in a controller route, all those attributes can be passed right into the erb/view file:

```
# views/recipes/show.erb

<h1><%= @recipe.title %></h1>
<p><%= @recipe.description %></p>

<h2>Ingredients</h2>
<ul>
<% @recipe.ingredients.each do |ingredient| %>
  <li><%= ingredient %></li>
<% end %>
</ul>

<h2>How to Cook</h2>
<p><%= @recipe.method %></p>
``` 

**Setting up a POST route for a form**

```
get '/recipes/new' do
  erb :'recipes/new'
end
```

controller sets up the form url

```
# views/recipes/new.erb

<form method='POST' action='/recipes'> 
  <label for="title">Title</label>
  <input type="text" name="title">

  <label for="description">Description</label>
  <textarea name="description"></textarea>

  <label for="ingredients">Ingredients</label>
  <textarea name="ingredients"></textarea>

  <label for="method">How to Cook</label>
  <textarea name="method"></textarea>

  <input type="submit" value="Submit">
</form>
```

- important bit: method='POST' action='/recipes  
-> the action attribute tells the controller which route should handle the form; the method sets the POST request
- the name attribute on each input tag -> sets up the params hash which will look like this:

```
{ 
  "title" => "Apple Pie",
  "description" => "A recipe that I learned from my granny.",
  "ingredients" => "4 apples, 1 cup sugar, ...",
  "method" => "Preheat oven to 350 degrees. Cut the apples in small pieces..." 
}
```

- the controller bit that handles this POST data:

```
# This is responsible for PROCESSING a newly submitted recipe form
post '/recipes' do
  @recipe = Recipe.new

  # get data from params
  @recipe.title = params[:title]
  @recipe.descriptions = params[:descriptions]
  @recipe.ingredients = params[:ingredients]
  @recipe.method = params[:method]
  @recipe.save
  
   # show post after completion
  redirect "/recipes/#{@recipe.id}"
end
```

- the last line redirects user to a page to avoid blank page

## Sinatra:

- add to your Gemfile and require it in the code, bundle 
- [documentation](http://sinatrarb.com/intro.html)
- view app in browser on http://localhost:4567
- anatomy of a Sinatra app:

```
require 'sinatra'

get '/' do
  'hello!'
end
```

- the get is the method passed to the server (like GET, POST); the '/' is part of the path - in this case, the home page; the do-end block inside gets executed
- adding HTML & CSS to your Sinatra app:

```
require 'sinatra'
get '/cat' do
  "<div style='border: 3px dashed red'>
     <img src='http://bit.ly/1eze8aE'>
   </div>"
end
```

- separate views: add a views directory to your project, create an index.erb file in it; now refactor the above like this:

```
require 'sinatra'

get '/cat' do
  erb(:index)
end
```

## erb templating system:

- part of the Ruby Standard Library 
- [tutorial](https://www.stuartellis.name/articles/erb/)
- whatever is put between those tags gets executed (say inside a string that is visible on your page):

```
<%= %>
```

- sample:

```
erb "Hi there, Visitor <%= 2 + 2 %>!"
# => "Hi there, Visitor 4!"
```

### setting up test suite

- adding stuff to spec_helper - find Setup instructions for Capybara/other tools in their documentation; for Sinatra pick the Rack setup instructions
- the RACK_ENV environment variable sets to production on deployment, to test when set in the spec_helper 

## Adding a style sheet to Sinatra app

- create a public directory
- add img, sheets and other directories to hold the style elements 
- in lib, create a layout.erb - this will be where Sinatra looks for style tips before rendering each view (technically a view that holds other views, and tells the controller how to render them??)
- add this in layout.erb:

```
<!DOCTYPE html>
 <html>
  <head>
	  <title>Poke Battle</title>
	  <link href="<%= url('/style.css') %>" rel="stylesheet" type="text/css" />  
  </head>
  <body>
	  <h1>Testing layout.ERB!</h1>
	  <%= yield %>
  </body>
</html>
```

- the <%= yield %> is where all other erbs/views will be rendered - whatever is above yield is a fixed element of the app/will appear on every page
- setting up Sinatra in Sinatra Modular Style:

```
# in app.rb

require 'sinatra/base'

class Battle < Sinatra::Base
  get '/' do
    'Hello Battle!'
  end

  # start the server if ruby file executed directly
  run! if app_file == $0
end
```

## Sessions:

- in Sinatra, session is a hash stored on the server
- use redirect '/route' at the end of your post blocks - it issues an internal GET request
- session secret must be set for Shotgun to work!!

## Web helpers:

- gets added as a web_helpers.rb file in features
- require it in spec_helper
- define methods that follow the steps that are repeated in tests - make sure the method names are meaningful!
- call the method in your feature test file


### Refactoring to dos (more in [README](https://github.com/aniasobo/poki-battle/blob/master/README.md)):

- [x] single Player class - each player to be a separate instance of this class
- [ ] add unit tests for each view that use mocks and stubs 
- [ ] add instructions to README
- [ ] add metaprogramming to get rid of the global variable:

```
def self.create(player_1, player_2)
  @game = Game.new(player_1, player_2)
end

def self.instance
  @game
end

#called like this:

@game = Game.instance
```