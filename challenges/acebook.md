# Acebook challenge

## Agile

**sprints & estimation**

SCRUM:

1. backlog refinement - acceptance criteria for each ticket, tickets broken down, estimated time-wise
2. sprint planning - setting sprint goal from user POV
3. stands - update on progress of work, planned work and blockers
4. sprint review - product owner reviews current product
5. sprint retrospective - product owner gives feedback on review (not present at the retro), team discusses feedback/progress

roles:
- product owner
- scrum master
- dev

**working on branches**

- two approvals before merge
- unique # for tickets and branches (# of the trello ticket)

## Development workflow

1. Create a Github issue in the relevant repository 
2. When you are ready to work on the user story, create a branch
3. implement the user story
4. create a pull request from your branch to master
5. Get another member of the team to review your PR.
6. Use the pull request comments section to discuss the code and make improvements until the code reviewing pair are satisfied.
7. merge your PR.
8. merge your changes on GitHub. You should then deploy immediately. If you have CI setup you can get it to do this for you automatically.
9. Do some QA on your live site if you have it set up.

---  

## To discuss at sprint planning on Wed:

- pairing schedule
- leads for standup/retros
- keeping notes as team procedure
- 


## Rails command line tricks:

you can run the rails console directly on heroku with `heroku run rails console`  

you can run the rails console on pry instead of irb using the [pry-rails gem](https://github.com/rweng/pry-rails)  

apply migrations to the production db: `heroku run rake db:migrate`

retrieve the production db to use locally: `heroku db:pull postgres://username:password@localhost/dbname`  

push your local db to production (overwrites prod db): `heroku db:push`

initialise heroku db: `heroku run rake db:schema:load`



## Rails tutorial 

install with rvm  
`rails server` runs development server on port 3000  
`rails new` creates new project folder  
app directory is where the code lives  
db folder for migrations  
`rails generate model player name:string age:integer` - the generated model has Active Record hooked up automatically  
`rake db:migrate` - automatically executes db/migrations  
`rails console` - runs rails console (like a rails irb) in terminal  
class methods (.create, .all etc) automatically execute SQL queries (you don't have to write the class methods!!)  
add `def change` method to migrations to alter table, then run `rake db:migrate`  
always run migration first, then update schema  
`rake db:migrate:status` to view current status of migrations  
validations - built in to Rails, you just choose which fields to validate  
every setting - like validation - can be immediately tested in the rails console with no require; `reload!` in the console to update it with latest changes, but you have to always create a new object  
`objectname.errors.full_messages` to view the error messages after attempting an illegal action in console  
associations - in your classes descended from AR::Base; has_many, has_one, belongs_to etc  `has_many :players, through :something`  
`rails g model team` happens outside of the rails console  
`rails generate migration descriptiveNameOfMigration` then `rake db:migrate`, then update schema; once the model is updated & console reloaded, we can use the new methods  
many-to-many relationships: testing is crucial to make sure everything that has relationships gets updated  
view & controller:      
 
  
## Setting up Travis CI:

[this tutorial](https://medium.com/full-taxx/how-to-setup-travis-ci-for-a-rails-application-78a453963300)

**Procfile**

tells Heroku to run the server?
should have `rake run db:migrations` to migrate the db/migrate on each deploy?

[locales exemplar for GB](https://github.com/svenfuchs/rails-i18n/blob/master/rails/locale/en-GB.yml)
[from here](https://github.com/svenfuchs/rails-i18n)


## Rails rake tasks:

to view all your rake tasks: `$ rake -T` 

**Resources:**

[rake documentation](https://www.stuartellis.name/articles/rake/)

[good guide to rake](https://dev.to/vinistock/customizing-rails-rake-tasks-3bg5) 

[rake best pracices](https://edelpero.svbtle.com/everything-you-always-wanted-to-know-about-writing-good-rake-tasks-but-were-afraid-to-ask)

[recent guide to rake](https://www.rubyguides.com/2019/02/ruby-rake/)


**rake generator**

```
$ rails g task my_namespace
$ create lib/tasks/my_namespace.rake
```

this wil generate:

```
namespace :my_namespace do
  desc "TODO"
  task :my_task1 => :environment do
  end

  desc "TODO"
  task :my_task2 => :environment do
  end
end
```

**sample rake tasks:**

`rake -D time` for a list of tasks for finding time zone names. Default is UTC.

`rake my_task` runs the named task (seems to be running the namespace but not the task).  

`rake` runs all .rake files (but not specific tasks? 🤔 )


**rake task definition:** 

1. A description (desc-task-end block)
2. The name that identifies the task (:symbol)
3. The code to be executed by the task
*  optional input parameters and other tasks that are prerequisites.

sample: 
```
namespace :test
	desc "One line task description"
	task :name_of_task do
	  # Your code goes here
	end
end
```

sample task that depends on other tasks:
```
namespace :main do
  task :test do
    if true
      puts "Calling test2 task."
      Rake::Task["main:test2"].invoke #invokes main:test2
    else
      abort()
    end
  end

  task :test2 do
      puts ">Test2 task invoked"
  end
end
```

sample task with parameters:
```
desc "Example of task with parameters and prerequisites"
task :my_task, [:first_arg, :second_arg] => ["first_task", "second_task"] do |t, args|
  args.with_defaults(:first_arg => "Foo", :last_arg => "Bar")
  puts "First argument was: #{args.first_arg}"
  puts "Second argument was: #{args.second_arg}"
end
```

to run the above task you must specify the values: `rake my_task[one,two]`

```
namespace :import do
	desc "imports data from csv file"
	task :data => :environment do
		require 'csv'
		CSV.foreach('path/to/products.csv') do |row|
			name = row[0]
			price = row[1].to_i
			Product.create(name: name, price: price)
		end
	end
end
```

`rake import:data` to run the data task from the import namespace

**one-off tasks:**

keep in tasks without executing.

[option to test any added rake tasks](http://blog.jayfields.com/2006/11/ruby-testing-rake-tasks.html)

to execute: `rake test_task:only_run_when_told` where `test_task` is name of namespace and `only_run_when_told` is name of task.

added the above to Travis.yml to force Travis to execute custom task - outcome: failed, trying with `bundle exec rake` in Travis.yml
adding this line in Travis.yml under scripts worked: `bundle exec rake test_task:only_run_when_told`


**TO DO**

Adding a rake task to clear the database.

```
gem 'database_cleaner' # added in dev or staging group
```

then generate `rails g task clean`


```
# tasks/db/clean.rake

namespace :db do

  desc "Truncate all existing data"
  task :truncate => "db:load_config" do
    DatabaseCleaner.clean_with :truncation
  end

end
```

**add tasks to Procfile for Heroku to execute:**

`worker: bundle exec rake my:rake_task`

added: `release: bundle exec rake db:migrate`

- [x] add DS store to gitignore and unstage

---

## the asset pipeline

WebPack - will come by default with Rails 6;

`$ rails` displays all available rake and rails commands

in app/assets/config/manifest.js - a series of comment-like links that are not comments! 

every asset file that you want included in the application.html.erb view has to go within those tags:

```
<%= csrf_meta_tags %>

<%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true %>
<%= javascript_include_tag 'application' %>
```

adding stuff like bootstrap: add bs files in vendor directory, with all the naming conventions of the app directory preserved, then in manifest, add `//= bootstrap.js` and `//= bootstrap.css`, then possibly add a root in the config/environments/initializers/assets.rb so that rails knows what to compile.

config/environments directory is where you can configure your precompilers for each environment.

> what the heck is precompiling assets? ¯\_(⊙︿⊙)_/¯ 

precompiling assets should be done on production for performance reasons.

`<%= image_tag "img_name.jpg", alt: "alt text", width: 300, class: "class-name" %>` - within html, not enclosed by any other tags.

for random assets not in the images folder but in the assets directory somewhere:

`<%= asset_path "img_name.jpg" %>`

how to use assets from the images folder in your CSS:

```
body {
  background-image: image-url('file.jpg');
}
```

[Awesome pre-programmed CSS gradients to use](https://uigradients.com)

---  

[a half-decent explanation of the asset pipeline](https://www.youtube.com/watch?v=kUuD41mTPkE) 

### The three places that matter in the asset pipeline:

1. app/assets
2. lib/assets
3. vendor/assets (need more tweaking in config files as they're not native)

**asset pipeline helpers**

the stuff that goes on top of the other tags in erbs, for example `<%= stylesheet_link_tag %>` or `<%= javascript_include_tag %>`

image_tag helper can go anywhere within the view.

adding a custom stylesheet: in assets/stylesheets, named like: `erbexample.css.erb` or `example.css.scss`, then require it with the appropriate helper tag in the erb.

`asset_path` helper can be used throughout.

## Week 2 TO DO:

- [ ] add FactoryBot - good [cheatsheet](https://devhints.io/factory_bot)


`bin/rails routes` to see all your routes (routing debugging)


## Comments to dos:

- [x] display user name in comment instead of Anonymous
- [x] style the new comment form better
