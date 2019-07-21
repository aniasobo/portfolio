# Instagram challenge

## Initializing a new rails project on top of a fork:

`rails new instagram-challenge -s` from projects folder - keeps all the existing files in that directory, adding rails scaffold on top.

`rails new --help` to view options available with the `rails help` command for initialising a new Rails project.  

`bundle install` revealed that the rubocop gem's version had to be changed for the project.

`rails generate rspec:install` to initialise rspec (if `rspec init` was run before, use this one to overwrite it)

added DS_Store too .gitignore as usual: `/**/.DS_Store` - possibly should be in a `~/.gitignore_global` ?

## Coding!

Going by [this tutorial](https://pusher.com/tutorials/photo-sharing-ruby-rails), I generate my posts model with `rails generate model Post link:text caption:text`, then run `rails db:migrate`.

I then generate my controller with `rails generate controller Photo index store`; this generates: 

- view for Photo index
- view for Photo store
- the Photos controller
- the route
- unit test for the Photo controller
- helper file
- asset for adding JS and CSS to Photos

Moving on to the index view - added CSS for photo index.

Routing of the POST route from photo upload

- added dotenv gem with `.vars.env` file to store API keys for Cloudinary, which I also added as a gem to store my photos
- those environment variables are intended for the development environment; production vars will be added to the heroku config 

**TIP!**

Create a Rails app that runs on PostGreSQL from the get go with `rails new my_app_name --database=postgresql`

**TIP!**

To clear production database, run this in terminal: `heroku restart; heroku pg:reset DATABASE --confirm fauxtagram; heroku run rake db:migrate`