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