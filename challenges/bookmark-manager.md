# Bookmark manager

_Makers Academy Week 4 challenge_

## Functionality:

- [x] Show a list of bookmarks
- [ ] Add new bookmarks
- [ ] Delete bookmarks
- [ ] Update bookmarks
- [ ] Comment on bookmarks
- [ ] Tag bookmarks into categories
- [ ] Filter bookmarks by tag
- [ ] Users are restricted to manage only their own bookmarks

## Steps:

- [x] Creating User Stories
- [x] Setting up a Web Project
- [x] Viewing bookmarks
- [x] Setting up a Database
- [x] Creating your First Table
- [x] Manipulating Table Data
- [x] Interacting with Postgres from Ruby
- [ ] Upgrading your Toolset
- [ ] Setting up a Testing Environment
- [ ] Creating bookmarks
- [ ] Wrapping Database data in program objects
- [ ] Deleting bookmarks
- [ ] CRUD
- [ ] Extracting a Database Setup object
- [ ] Validating bookmarks
- [ ] One to Many Relationships
- [ ] Many to Many Relationships
- [ ] Registration
- [ ] Authentication


### Concepts practiced:

- user stories - guided by this [Pill](https://github.com/makersacademy/course/blob/master/pills/user_stories.md) and [gov.uk](https://www.gov.uk/service-manual/agile-delivery/writing-user-stories)
- setting up Sinatra with Capybara and rspec
- adding images to README straight from the repo images folder


### Approach:

- app.rb - controller
- bookmark_manager - the BookmarkManager class
- database: bookmarkmanager
- table: bookmarks (id as primary key, url with max 60 characters)