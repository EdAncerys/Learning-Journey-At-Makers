# Week 4 Goals 

#### By the end of the week all developers can:

- Build a simple web app with a database
- Follow an effective debugging process for database applications
- Explain the basics of how databases work (e.g. tables, SQL, basic relationships)

## Daily Goals 
### Monday 04 of May 2020

## Morning Goals 

- Code Review for the weekend challenge.
- Attend week 4 *kick off*. **Database** work shop. 
- Set a working plan for the new week

##### Plan:

- Review weekend challenge in pair
- Set goals for the new week
  
**Process:** 

Main focuses for this week

- Agile and TDD
- Engineering and 'Dev Recipes'
- Databases
- Tooling

Code Review for the weekend [**RPS Challenge:**](https://github.com/EdAncerys/rps-challenge)

**Plan:** Peer code review of the weekend challenge. Will be reviewing and getting a feedback to Gareth's code.

**Process:**   
- Start with making an appreciation about Gareth's code.
- Write at least one piece of constructive feedback.
- Spend time implementing those changes.

**What I've learned:**  

> Can redirect user to different view depending on outcome by adding simple logic to the controller:

```rb
 post '/choice_selected' do
    @game = Game.instance
    @game.current_player.choice = params[:choice]
    redirect '/end_game' if @game.all_players_selected?
    # Code continues 
```

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"Bookmark Manager"**](https://github.com/EdAncerys/bookmark-manager)

**Plan:** Pair with Marius and keep working on the afternoon challenge for the week - *"Bookmark Manager".*

**Process:**

- Creating User Stories. Domain model for it as per bellow: 

<p align="center">
    <img width="600" src="images/Bookmark_Manager_01.png">  
    *Domain Model for Bookmark App* 
</p>

- Set up **Sinatra with RSpec and Capybara**
Adding feature test for view: 

```rb
feature 'Viewing bookmarks' do
  scenario 'visiting the index page' do
    visit('/')
    expect(page).to have_content "Bookmark Manager"
  end
end
```
Setting up **controller** (`app.rb`) and route for view.
- Next user story leads to have bookmarks in the view. Adding feature test to test drive our code:

```rb
# in spec/features/viewing_bookmarks_spec.rb

feature 'Viewing bookmarks' do
  scenario 'A user can see bookmarks' do
    visit('/bookmarks')

    expect(page).to have_content "http://www.makersacademy.com"
    expect(page).to have_content "http://www.destroyallsoftware.com"
    expect(page).to have_content "http://www.google.com"
  end
end
```
After adding array directly to the controller appropriate route we create our view by adding following html code:

```rb
<!-- in views/bookmarks/index.erb -->

<ul>
  <% @bookmarks.each do |bookmark| %>
    <li><%= bookmark %></li>
  <% end %>
</ul>
```
Ability to have all bookmarks displayed we can write our feature tests again to test drive our code as follows:  

```rb
require 'bookmark'

describe Bookmark do
  describe '.all' do
    it 'returns all bookmarks' do
      bookmarks = Bookmark.all

      expect(bookmarks).to include("http://www.makersacademy.com")
      expect(bookmarks).to include("http://www.destroyallsoftware.com")
      expect(bookmarks).to include("http://www.google.com")
    end
  end
end
```
Now that we have this class, we can require it in app.rb, which becomes:

```rb
require 'sinatra/base'
require './lib/bookmark'

class BookmarkManager < Sinatra::Base
  get '/bookmarks' do
    @bookmarks = Bookmark.all
    erb :'bookmarks/index'
  end

  run! if app_file == $0
end
```

- Setting database with **PostgreSQL** to store bookmark list. To full-fill our next user story we have to set up `psql` database by running the following command in terminal(Mac OS):

```
brew install postgresql
```
PostgreSQL is a database management service. It's handy to keep PostgreSQL running 'in the background'. This command will start PostgreSQL in the background and restart it when you login:

```
$ brew services start postgresql
```
To start psql, type psql <database name> into a Terminal, where <database name> is the name of the database you want to interact with.

```
$ psql postgres
postgres=#
```
Create a database using SQL:

```
postgres=# CREATE DATABASE "your_user_name_here";

```

Listing all database tables:

```
postgres=# \l
```

- To create new database we run the following command:

```
admin=# CREATE DATABASE DATABASE_NAME;
```
As we have now database created we can connect to it and create tables to store data by doing the following:

```
admin=# \c bookmark_manager;
```
We're going to make a bookmarks table that will store bookmarks from our application. We can use SQL commands from psql:

```
bookmark_manager=# CREATE TABLE bookmarks(id SERIAL PRIMARY KEY, url VARCHAR(60));
```

- **Manipulating Table data**.  
Using `INSERT` to add data to the table.

```
bookmark_manager=# INSERT INTO bookmarks VALUES(1, 'http://www.makersacademy.com');
```

 Using `SELECT` to query data:
 
 ```
 bookmark_manager=# SELECT * FROM bookmarks;
 ```
 Using `DELETE` to delete data 
 
 ```
 DELETE FROM bookmarks WHERE url = 'http://www.twitter.com';
 ```
 Using `UPDATE` to update data
 
 ```
 UPDATE bookmarks SET url = 'http://www.destroyallsoftware.com' WHERE url = 'http://www.askjeeves.com';
 ```
- Interacting with PostgreSQL from Ruby by adding psql `gem` to *Gemfile*:

```rb
# Inside Gemfile

source "https://rubygems.org"

gem 'pg'
gem 'sinatra'

gem 'capybara', group: :test
gem 'rspec', group: :test
```

- **Connecting to the database**. This can be done by adding the following to *Bookmark* class:

```rb
# in lib/bookmark.rb

require 'pg'

class Bookmark
  def self.all
    connection = PG.connect(dbname: 'bookmark_manager')
    result = connection.exec('SELECT * FROM bookmarks')
    result.map { |bookmark| bookmark['url'] }
  end
end
```

**What I've Learned:**

> **What is a database?** A database is simply organised part of a filesystem. It's optimised for storing and retrieving data.

> **Is Postgres a database?** A common database system for modern web development is called PostgreSQL. PostgreSQL is actually a server that runs a database. Therefore, it can be started, stopped, and interacted with through an interface, psql.

> To start psql, type psql <database name> into a Terminal, where <database name> is the name of the database you want to interact with.
 ```
$ psql postgres
postgres=#
```
> The spec/spec_helper.rb is automatically executed whenever you run rspec (see your .rspec for why). In the Spec Helper, you can configure RSpec. You can make something happen before every spec with the following:
```rb
config.before(:each) do
  # Whatever you put here will happen before each spec runs.
end
```

## Daily Goals 
### Tuesday 5 of May 2020

## Morning Goals 

#### Databases.

**Plan:**

- Perform research online individually.  
- Describe what **Database** is and it's usages. 
- Summarize and give some practical example. 
  
**Process:** 

A database is an organized collection of structured information, or data, typically stored electronically. A database is usually controlled by a database management system (DBMS). The DBMS, along with the applications that are associated with them, are referred to as a database system or **database** for short.

Data is typically modeled in rows and columns in a series of tables to make processing and data querying efficient. The data can then be easily accessed, managed, modified, updated, controlled, and organized. Most databases use **structured query language (SQL)** for writing and querying data.

- Every database has a **DBMS** (Database Management System) which structures how we organize and interact with all our stored data. Four fundamental ways of interaction with databases: **(CRUD)**
  - Create
  - Read
  - Update
  - Delete
  
- This DBMS can be:
  - Relational: organizes data in tables made of columns and rows (columns are categories and each row inside them holds a data entry). They are highly structured and have strict data types. Great for managing complex datasets. We talk to them using SQL (Structured Query Language).
  
  - Non-Relational: also known as noSQL (we don't use SQL to talk to them). These are more flexible systems with less strictness around data types (graphs, key-values...). They are good for getting a database up and running quickl and for deploying data across decentralised distributed networks (when data is stored across many computers that all hae to coordinate with each other).
  
- Most popular DMS:

1. Oracle
2. MySQL
3. Microsoft SQL
4. PostgreSQL
5. MongoDB (noSQL)

**What I've Learned:**

> Data is typically modeled in rows and columns in a series of tables to make processing and data querying efficient.

> **SQL** (Structured Query Language) standard language used to communicate with a database. SQL statements are used to perform tasks such as update data on a database, or retrieve data from a database.

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"Bookmark Manager"**](https://github.com/EdAncerys/bookmark-manager)

**Plan:** Pair with Jed and keep working on the afternoon challenge for the week - *"Bookmark Manager".*

**Process:**

- Setting up a testing environment (**Test database**). A test environment that runs locally on your computer whenever you run your tests. It comes handy for tests that need to have predictable outcome.

To set up *test database* we need to run following commands in terminal:

```
$> psql DATABASE_NAME (or postgresql)
admin=# CREATE DATABASE "bookmark_manager_test";
admin=# CREATE TABLE bookmarks(id SERIAL PRIMARY KEY, url VARCHAR(60));
```
We need to add following code to our `spec_helper.rb` :

```
# in spec/spec_helper.rb

ENV['ENVIRONMENT'] = 'test'
```

As `spec_hlper.rb` always run first before any test we can tel **RSpec** to load/look in to test environment only. 

We can now use this omnipresent ENV variable in our Bookmark class, to determine which database we should connect to:

```rb
# in lib/bookmark.rb
require 'pg'

class Bookmark
  def self.all
    if ENV['ENVIRONMENT'] == 'test'
      connection = PG.connect(dbname: 'bookmark_manager_test')
    else
      connection = PG.connect(dbname: 'bookmark_manager')
    end

    result = connection.exec("SELECT * FROM bookmarks")
    result.map { |bookmark| bookmark['url'] }
  end
end
```

**Tests should always run against an empty database**. We should set up any required Test data in the test itself. Let's write a script that sets up and clears out the test database each run.

We need to 'drop' the database between each run of the script. Let's use PostgreSQL's TRUNCATE command to do that:

```rb
require 'pg'

p "Setting up test database..."

def setup_test_database 
  connection = PG.connect(dbname: 'bookmark_manager_test')
  # Clear the bookmarks table
  connection.exec("TRUNCATE bookmarks;")
end
```
Integrate the script into our test runner, `rspec` by adding following to `spec_helper.rb` :

```rb
require_relative './setup_test_database'

ENV['ENVIRONMENT'] = 'test'

RSpec.configure do |config|
  config.before(:each) do
    setup_test_database
  end
end
```
- Creating bookmarks and adding them to database.
Write a feature test for adding bookmarks should look like this:

```rb
# in spec/features/creating_bookmarks_spec.rb

feature 'Adding a new bookmark' do
  scenario 'A user can add a bookmark to Bookmark Manager' do
    visit('/bookmarks/new')
    fill_in('url', with: 'http://testbookmark.com')
    click_button('Submit')

    expect(page).to have_content 'http://testbookmark.com'
  end
end
```

We should use a POST route to define this route, as we're submitting data to the application to be saved. Our view should look like:

```
<form action="/bookmarks" method="post">
  <input type="text" name="url" />
  <input type="submit" value="Submit" />
</form>
```

Let's define this POST route, and print to the console whenever the route is activated:

```rb
get '/bookmarks/new' do
  erb :"/bookmarks/new"
end

post '/bookmarks' do
  Bookmark.create(url: params['url'])
  redirect '/bookmarks'
end
```
Adding **Unit test** to test our model method:

```rb
# in spec/bookmark_spec.rb

describe '.create' do
  it 'creates a new bookmark' do
    Bookmark.create(url: 'http://www.testbookmark.com')

    expect(Bookmark.all).to include 'http://www.testbookmark.com'
  end
end
```
Now we can finally add write method that pass the **Unit tats** and code looks like:
```rb
# in lib/bookmark.rb

def self.create(url:)
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end

  connection.exec("INSERT INTO bookmarks (url) VALUES('#{url}')")
end
```
- Wrapping database data in program objects. 

At the moment, when we use Bookmark.all to get bookmarks from the database, we just return an array of strings.

In this challenge, you will add a title column to the bookmarks table, and display it on the homepage instead of the link URL. To do this, you will need to wrap database data in a Ruby object.

Before we can make any changes to the application features, the bookmarks table needs to be updated to accept a title value.

To make this change in the bookmark_manager database via psql, use the following command:
```
ALTER TABLE bookmarks ADD COLUMN title VARCHAR(60);
```
We'll need to save this step in the db/migrations directory:

```
# in db/migrations/02_add_title_to_bookmarks.sql

ALTER TABLE bookmarks ADD COLUMN title VARCHAR(60);
```

Adding title to creating a bookmark

Before a user can see the title of a bookmark, they'll need to be able to add the title. Let's start by updating the feature test for creating bookmarks:

```rb
# in spec/features/creating_bookmarks_spec.rb

feature 'Adding a new bookmark' do
  scenario 'A user can add a bookmark to Bookmark Manager' do
    visit('/bookmarks/new')
    fill_in('url', with: 'http://www.testbookmark.com')
    fill_in('title', with: 'Test Bookmark')
    click_button('Submit')

    expect(page).to have_link('Test Bookmark', href: 'http://www.testbookmark.com')
  end
end
```

We'll need to add this additional field to the bookmarks/new view:

```
<!-- in views/bookmarks/new.erb -->
<form method="post" action="/bookmarks/new">
  <input type="text" name="url" placeholder="URL" />
  <input type="text" name="title" placeholder="Title" />
  <input type="submit" value="Submit" />
</form>
```
And let's pass this new field to Bookmark.create in the Controller:

```rb
# in app.rb

post '/bookmarks/new' do
  Bookmark.create(url: params[:url], title: params[:title])
  redirect '/bookmarks'
end
```
Now the data can be collected, we want to update Bookmark.create to save a bookmark title in addition to the url. Let's update the test to reflect this:

```
# in spec/bookmark_spec.rb

require 'database_helpers'

describe '.create' do
  it 'creates a new bookmark' do
    bookmark = Bookmark.create(url: 'http://www.testbookmark.com', title: 'Test Bookmark').first

    expect(bookmark['url']).to eq 'http://www.testbookmark.com'
    expect(bookmark['title']).to eq 'Test Bookmark'
  end
end
```
Now let's update Bookmark.create to pass the title to the database. We need the SQL query to return the Bookmark we're creating, so we can check that the Bookmark has been created with the given values. This also removes any dependency on the .all method.

```rb
def self.create(url:, title:)
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end
  result = connection.exec("INSERT INTO bookmarks (url, title) VALUES('#{url}', '#{title}') RETURNING id, title, url;")
  Bookmark.new(id: result[0]['id'], title: result[0]['title'], url: result[0]['url'])
end
```

Updating feature test to show title in the /bookmarks view:

```rb
feature 'viewing bookmarks' do
  scenario 'bookmarks are visible' do
    Bookmark.create(url: 'http://www.makersacademy.com', title: 'Makers Academy')
    Bookmark.create(url: 'http://www.destroyallsoftware.com', title: 'Destroy All Software')
    Bookmark.create(url: 'http://www.google.com', title: 'Google')

    visit '/bookmarks'

    expect(page).to have_link('Makers Academy', href: 'http://www.makersacademy.com')
    expect(page).to have_link('Destroy All Software',  href: 'http://www.destroyallsoftware.com')
    expect(page).to have_link('Google', href: 'http://www.google.com')
    end
  end
```
Adding a **Unit test** to test drive our model code: 

```rb
# in spec/bookmark_spec.rb

describe '.all' do
 it 'returns a list of bookmarks' do
   connection = PG.connect(dbname: 'bookmark_manager_test')

   # Add the test data
   bookmark = Bookmark.create(url: "http://www.makersacademy.com", title: "Makers Academy")
   Bookmark.create(url: "http://www.destroyallsoftware.com", title: "Destroy All Software")
   Bookmark.create(url: "http://www.google.com", title: "Google")

   bookmarks = Bookmark.all

   expect(bookmarks.length).to eq 3
   expect(bookmarks.first).to be_a Bookmark
   expect(bookmarks.first.id).to eq bookmark.id
   expect(bookmarks.first.title).to eq 'Makers Academy'
   expect(bookmarks.first.url).to eq 'http://www.makersacademy.com'
  end
end
```
Use this test to drive the update to the Bookmark.all method:

```rb
def self.all
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end
  result = connection.exec("SELECT * FROM bookmarks")
  result.map do |bookmark|
    Bookmark.new(id: bookmark['id'], title: bookmark['title'], url: bookmark['url'])
  end
end
```
Returning a bookmark from Bookmark.create by doing the following:

```rb
# in spec/bookmark_spec.rb
require 'database_helpers'

describe '.create' do
  it 'creates a new bookmark' do
    bookmark = Bookmark.create(url: 'http://www.testbookmark.com', title: 'Test Bookmark')
    persisted_data = persisted_data(id: bookmark.id)

    expect(bookmark).to be_a Bookmark
    expect(bookmark.id).to eq persisted_data['id']
    expect(bookmark.title).to eq 'Test Bookmark'
    expect(bookmark.url).to eq 'http://www.testbookmark.com'
  end
end
```

Let's refactor the test to extract a persisted_data helper method:
```rb
# in spec/database_helpers.rb
require 'pg'

def persisted_data(id:)
  connection = PG.connect(dbname: 'bookmark_manager_test')
  result = connection.query("SELECT * FROM bookmarks WHERE id = #{id};")
  result.first
end
```
- Deleting Bookmarks.

Here's the user flow for deleting a bookmark:

- Visit the bookmarks page.
- Click a 'delete' button next to a bookmark.
- See the bookmarks page, without that bookmark.

Here's that flow in Capybara terms:
```rb

# in spec/features/deleting_a_bookmark_spec.rb

feature 'Deleting a bookmark' do
  scenario 'A user can delete a bookmark' do
    Bookmark.create(url: 'http://www.makersacademy.com', title: 'Makers Academy')
    visit('/bookmarks')
    expect(page).to have_link('Makers Academy', href: 'http://www.makersacademy.com')

    first('.bookmark').click_button 'Delete'

    expect(current_path).to eq '/bookmarks'
    expect(page).not_to have_link('Makers Academy', href: 'http://www.makersacademy.com')
  end
end
```
To add this feature we need to update view:

```
<ul>
  <% @bookmarks.each do |bookmark| %>
    <li class="bookmark" id="bookmark-<%= bookmark.id %>">
      <a href="<%= bookmark.url %>" target="_blank">
        <%= bookmark.title %>
      </a>
      <form action="/bookmarks/<%= bookmark.id %>" method="post">
        <input type='hidden' name='_method' value='DELETE'/>
        <input type="submit" value="Delete" />
      </form>
    </li>
  <% end %>
</ul>
```
We need to build a route for our Delete button to submit to, in app.rb, and enable :method_override (if you are using Sinatra::Base) so we can use the DELETE method.

```rb
# in app.rb

enable :sessions, :method_override

delete '/bookmarks/:id' do
  # let's print out the form params
  p params
end

```

We can use this to write the SQL to delete the bookmark with that ID, and redirect:

```rb
# in app.rb

delete '/bookmarks/:id' do
  Bookmark.delete(id: params[:id])
  redirect '/bookmarks'
end
```
Now that our test passes, let's move the SQL into the Bookmark model. Start with a spec for Bookmark.delete:

```rb
# in spec/bookmark_spec.rb

describe '.delete' do
  it 'deletes the given bookmark' do
    bookmark = Bookmark.create(title: 'Makers Academy', url: 'http://www.makersacademy.com')

    Bookmark.delete(id: bookmark.id)

    expect(Bookmark.all.length).to eq 0
  end
end
```
And code that looks something like:

```rb
class Bookmark
  def self.delete(id:)
    if ENV['ENVIRONMENT'] == 'test'
      connection = PG.connect(dbname: 'bookmark_manager_test')
    else
      connection = PG.connect(dbname: 'bookmark_manager')
    end
    connection.exec("DELETE FROM bookmarks WHERE id = #{id}")
  end

  ### rest of the class ###
end
```

- Adding ability to update bookmarks.
We adding feature test. Here's that flow in Capybara terms:

```rb
# in spec/features/updating_a_bookmark_spec.rb

feature 'Updating a bookmark' do
  scenario 'A user can update a bookmark' do
    bookmark = Bookmark.create(url: 'http://www.makersacademy.com', title: 'Makers Academy')
    visit('/bookmarks')
    expect(page).to have_link('Makers Academy', href: 'http://www.makersacademy.com')

    first('.bookmark').click_button 'Edit'
    expect(current_path).to eq "/bookmarks/#{bookmark.id}/edit"

    fill_in('url', with: "http://www.snakersacademy.com")
    fill_in('title', with: "Snakers Academy")
    click_button('Submit')

    expect(current_path).to eq '/bookmarks'
    expect(page).not_to have_link('Makers Academy', href: 'http://www.makersacademy.com')
    expect(page).to have_link('Snakers Academy', href: 'http://www.snakersacademy.com')
  end
end
```

Updated view looks like:
```
<!-- in views/bookmarks/index.erb -->

<ul>
  <% @bookmarks.each do |bookmark| %>
    <li class="bookmark" id="bookmark-<%= bookmark.id %>">
      <a href="<%= bookmark.url %>" target="_blank">
        <%= bookmark.title %>
      </a>
      <form action="/bookmarks/<%= bookmark.id %>" method="post">
        <input type='hidden' name='_method' value='DELETE'/>
        <input type="submit" value="Delete" />
      </form>
      <form action="/bookmarks/<%= bookmark.id %>/edit" method="get">
        <input type="submit" value="Edit" />
      </form>
    </li>
  <% end %>
</ul>
```

Let's define a route for this url:

```rb
# in app.rb

get '/bookmarks/:id/edit' do
  @bookmark_id = params[:id]
  erb :'bookmarks/edit'
end
```
And a view with the form:

```
<!-- in views/bookmarks/edit.erb -->

<form action="/bookmarks/<%= @bookmark_id %>" method="post">
  <input type="hidden" name="_method" value="PATCH" />
  <input type="text" name="url" />
  <input type="text" name="title" />
  <input type="submit" value="Submit" />
</form>
```

And another route, to which this form submits:

```
patch '/bookmarks/:id' do
  connection = PG.connect(dbname: 'bookmark_manager_test')
  connection.exec("UPDATE bookmarks SET url = '#{params[:url]}', title = '#{params[:title]}' WHERE id = '#{params[:id]}'")

  redirect('/bookmarks')
end
```

The first obvious refactor is to push the updating SQL into the model, using TDD you should end up with tests similar to this:

```rb
# in spec/bookmark_spec.rb

describe '.update' do
  it 'updates the bookmark with the given data' do
    bookmark = Bookmark.create(title: 'Makers Academy', url: 'http://www.makersacademy.com')
    updated_bookmark = Bookmark.update(id: bookmark.id, url: 'http://www.snakersacademy.com', title: 'Snakers Academy')

    expect(updated_bookmark).to be_a Bookmark
    expect(updated_bookmark.id).to eq bookmark.id
    expect(updated_bookmark.title).to eq 'Snakers Academy'
    expect(updated_bookmark.url).to eq 'http://www.snakersacademy.com'
  end
end
```
We can solve this by moving the controller SQL into the bookmark model:
```rb
# in lib/bookmarks.rb

def self.update(id:, url:, title:)
  if ENV['ENVIRONMENT'] == 'test'
    connection = PG.connect(dbname: 'bookmark_manager_test')
  else
    connection = PG.connect(dbname: 'bookmark_manager')
  end
  result = connection.exec("UPDATE bookmarks SET url = '#{url}', title = '#{title}' WHERE id = #{id} RETURNING id, url, title;")
  Bookmark.new(id: result[0]['id'], title: result[0]['title'], url: result[0]['url'])
end
```

Now our refactored routes for update and get will look like:

```rb
# in app.rb

patch '/bookmarks/:id' do
  Bookmark.update(id: params[:id], title: params[:title], url: params[:url])
  redirect '/bookmarks'
end

# in app.rb

get '/bookmarks/:id/edit' do
  @bookmark = Bookmark.find(id: params[:id])
  erb :"bookmarks/edit"
end
```

Let's write a Bookmark.find method to do that:

```rb
# in spec/bookmark_spec.rb

describe '.find' do
    it 'returns the requested bookmark object' do
      bookmark = Bookmark.create(title: 'Makers Academy', url: 'http://www.makersacademy.com')

      result = Bookmark.find(id: bookmark.id)

      expect(result).to be_a Bookmark
      expect(result.id).to eq bookmark.id
      expect(result.title).to eq 'Makers Academy'
      expect(result.url).to eq 'http://www.makersacademy.com'
    end
  end
end
```

Here's the implementation in Bookmark:

```rb
# in lib/bookmark.rb

class Bookmark
  def self.find(id:)
    if ENV['ENVIRONMENT'] == 'test'
      connection = PG.connect(dbname: 'bookmark_manager_test')
    else
      connection = PG.connect(dbname: 'bookmark_manager')
    end
    result = connection.exec("SELECT * FROM bookmarks WHERE id = #{id};")
    Bookmark.new(id: result[0]['id'], title: result[0]['title'], url: result[0]['url'])
  end

  ### rest of the class ###
end
```

Now we can use this Bookmark object in our form. We can set the value attribute of each input to the current value of the bookmark:

```rb
<!-- in views/bookmarks/edit.erb -->

<form action="/bookmarks/<%= @bookmark.id %>" method="post">
  <input type="hidden" name="_method" value="PATCH" />
  <input type="text" name="url" value="<%= @bookmark.url %>" />
  <input type="text" name="title" value="<%= @bookmark.title %>" />
  <input type="submit" value="Submit" />
</form>
    
```
**What I've Learned:**

We can set up an Environment Variable (**ENV**) to tell the application to use the test database when we run our tests

```rb
# in spec/spec_helper.rb

ENV['ENVIRONMENT'] = 'test'
```

> To build a route for Delete button to submit to, in app.rb, and enable :method_override (if you are using Sinatra::Base) so we can use the DELETE method.

```
enable :sessions, :method_override
```

> CRUD is an acronym for the four 'basic functions' of persistent storage:

>- Creating data
>- Reading data
>- Updating data
>- Deleting data

## Daily Goals 
### Wednesday 6 of May 2020

## Morning Goals 

#### Class methods vs instance methods.

**Plan:**

- Perform research online individually.  
- Describe what **class methods are** and there usages. 
- Summarize and give some practical example. 
  
**Process:** 

#### Difference between class methods and Instance methods

In Ruby, a method provides functionality to an Object. A class method provides functionality to a class itself, while an instance method provides functionality to one instance of a class.

- Class method are methods which require an object of its class to be created before it can be called. Class methods are the methods that can be called without creating an object of class.
- Class method is declared with static keyword. Instance method is not with static keyword.
- Class method means which will exist as a single copy for a class. But instance methods exist as multiple copies depending on the number of instances created for that class.
- Class methods can be invoked by using class reference (**self**). Class or non static methods are invoked by using object reference.
- Class methods can not access instance methods and instance variables directly. Instance method can access class variables and class methods directly.
- We cannot call an instance method on the class itself, and we cannot directly call a class method on an instance.

```rb
class SayHello
  def self.from_the_class
    "Hello, from a class method"
  end

  def from_an_instance
    "Hello, from an instance method"
  end
end
```

This would yield the following:

```
>> SayHello.from_the_class
=> "Hello, from a class method"

>> SayHello.from_an_instance
=> undefined method `from_an_instance' for SayHello:Class

>> hello = SayHello.new
>> hello.from_the_class
=> undefined method `from_the_class' for #<SayHello:0x0000557920dac930>

>> hello.from_an_instance
=> "Hello, from an instance method"
```

**What I've Learned:**

> Class methods can only be called on classes and instance methods can only be called on an instance of a class.

> **What does self mean?** Self is the currently executing receiver, the object to which a method is applied. A function-style method call implies self as the receiver.

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"Bookmark Manager"**](https://github.com/EdAncerys/bookmark-manager)

**Plan:** Pair with Patrick and keep working on the afternoon challenge for the week - *"Bookmark Manager".*

**Process:**

We will extract a `DatabaseConnection` object, and use it to set up a database connection on-boot. We'll use `DatabaseConnection` in the `Bookmark` class to act on the database, like this:

```ruby
# in bookmark.rb
require_relative 'database_connection'

class Bookmark
  def self.all
    result = DatabaseConnection.query("SELECT * FROM bookmarks")
    result.map { |bookmark| bookmark['url'] }
  end
end
```
- Extracting the database connection logic to an object

We're going to write a simple wrapper for the method `PG.connect`. It's going to be a class method, `setup`, on an object called `DatabaseConnection`.

Here's a test for that method:

```ruby
# in spec/database_connection_spec.rb

require 'database_connection'

describe DatabaseConnection do
  describe '.setup' do
    it 'sets up a connection to a database through PG' do
      expect(PG).to receive(:connect).with(dbname: 'bookmark_manager_test')

      DatabaseConnection.setup('bookmark_manager_test')
    end
  end
end
```

Here's the implementation of that class:

```ruby
# in lib/database_connection.rb

require 'pg'

class DatabaseConnection
  def self.setup(dbname)
    PG.connect(dbname: dbname)
  end
end
```

We should also write a test to ensure we can get the connection later on, through a class method called `connection`:

```ruby
# in spec/database_connection_spec.rb

it 'this connection is persistent' do
  # Grab the connection as a return value from the .setup method
  connection = DatabaseConnection.setup('bookmark_manager_test')

  expect(DatabaseConnection.connection).to eq connection
end
```

Here's the implementation for `DatabaseConnection` that solves this:

```ruby
# in lib/database_connection.rb

require 'pg'

class DatabaseConnection
  def self.setup(dbname)
    @connection = PG.connect(dbname: dbname)
  end

  def self.connection
    @connection
  end
end
```
- Using `DatabaseConnection` to set up a connection

When the application boots, we want the database connection to be setup. Therefore, let's:

- Require the `DatabaseConnection` into a script, `database_connection_setup.rb`
- Setup the database connection in this script, and
- Require this file into `app.rb`.

First, let's write a script in which we'll set up the database connection:

```ruby
# in database_connection_setup.rb

require './lib/database_connection'

if ENV['ENVIRONMENT'] == 'test'
  DatabaseConnection.setup('bookmark_manager_test')
else
  DatabaseConnection.setup('bookmark_manager')
end
```

Now, let's include the script in `app.rb`:

```ruby
# in app.rb

require 'sinatra/base'
require './lib/bookmark'
require './database_connection_setup'

class BookmarkManager < Sinatra::Base
   ### rest of the controller ###
end
```

- Adding a `query` method to `DatabaseConnection`

Let's add a `query` method to the `DatabaseConnection` object so we can use it to query the database. Here's the sort of code we want:

```ruby
# in bookmark.rb
require 'database_connection'

class Bookmark
  def self.all
    result = DatabaseConnection.query("SELECT * FROM bookmarks")
    result.map { |bookmark| bookmark['url'] }
  end
end
```

First, we write a test for `.query`:

```ruby
# in spec/database_connection_spec.rb

describe '.query' do
  it 'executes a query via PG' do
    connection = DatabaseConnection.setup('bookmark_manager_test')

    expect(connection).to receive(:exec).with("SELECT * FROM bookmarks;")

    DatabaseConnection.query("SELECT * FROM bookmarks;")
  end
end
```

We can pass this test by adding a `.query` class method to the `DatabaseConnection`. `query` just passes an SQL query string to the connection created by `setup`:

```ruby
# in lib/database_connection.rb

require 'pg'

class DatabaseConnection
  def self.setup(dbname)
    @connection = PG.connect(dbname: dbname)
  end

  def self.connection
    @connection
  end

  def self.query(sql)
    @connection.exec(sql)
  end
end
```

> Because the test for `query` relies explicitly on the persistent connection created by `setup`, we can now remove the `DatabaseConnection.connection` method (and test).

- Replace PG with our wrapper in `Bookmark`

Now that we've written a wrapper for PG, we can replace all calls to `PG` and `connection` with calls to this object, for example:

```ruby
# in lib/bookmark.rb

require 'database_connection'

class Bookmark
  def self.all
    result = DatabaseConnection.query("SELECT * FROM bookmarks")
    result.map do |bookmark|
      Bookmark.new(
        url: bookmark['url'],
        title: bookmark['title'],
        id: bookmark['id']
      )
    end
  end

  # rest of class

end
```
- Adding a feature test for an invalid URL

Here's the user flow for submitting an invalid URL:

1. Visit the new bookmark page.
2. Submit a new bookmark with a string like 'not a bookmark'.
3. See an error message, and don't see 'not a bookmark' in the list of bookmarks.

Here's that flow in Capybara terms:

```ruby
# in spec/features/adding_a_new_bookmark_spec.rb

scenario 'The bookmark must be a valid URL' do
  visit('/bookmarks/new')
  fill_in('url', with: 'not a real bookmark')
  click_button('Submit')

  expect(page).not_to have_content "not a real bookmark"
  expect(page).to have_content "You must submit a valid URL."
end
```

When we run this test, it fails as expected.

#### Passing the test, and adding Sinatra-Flash

```ruby
# in app.rb
require 'uri'

post '/bookmarks' do
  if params['url'] =~ /\A#{URI::regexp(['http', 'https'])}\z/
    Bookmark.create(url: params['url'], title: params[:title])
  else
    flash[:notice] = "You must submit a valid URL."
  end

  redirect('/bookmarks')
end
```

#### Refactoring the validation logic into the `Bookmark` model

Let's write a unit test for that:

```ruby
# in spec/bookmark_spec.rb

describe '.create' do
  it 'does not create a new bookmark if the URL is not valid' do
    Bookmark.create(url: 'not a real bookmark', title: 'not a real bookmark')
    expect(Bookmark.all).to be_empty
  end

  ### other tests been cut off ###
end
```
Validation into the `Bookmark.create` method. Let's split it out to a private method, too:

```ruby
# in bookmark.rb
require 'uri'

class Bookmark
  def self.create(url:)
    return false unless is_url?(url)
    result = DatabaseConnection.query("INSERT INTO bookmarks (url, title) VALUES('#{url}', '#{title}') RETURNING id, title, url;")
    Bookmark.new(id: result[0]['id'], title: result[0]['title'], url: result[0]['url'])
  end

  private

  def self.is_url?(url)
    url =~ /\A#{URI::regexp(['http', 'https'])}\z/
  end
end
```
Now we can use this updated `create` method in our controller:

```ruby
# in app.rb

post '/bookmarks' do
  flash[:notice] = "You must submit a valid URL." unless Bookmark.create(url: params[:url], title: params[:title])
  redirect('/bookmarks')
end
```

**What I've Learned:**

> We're using a _class instance variable_ to store the connection. We can do this because our `DatabaseConnection` is never going to be instantiated. It's a 'Singleton' object: there's only one `DatabaseConnection` in the application.

> The Flash is used to display one-time messages. To use the flash, we need to add the sinatra-flash gem to our Gemfile, install it to our project, and include sinatra/flash in our controller. Then, we need to enable :sessions.

## Daily Goals 
### Thursday 7 of May 2020

## Morning Goals 

#### Attend Database Domain Modeling using CRC cards with Josh.

**Plan:**

- Explain how to use CRC cards to model a domain
- Model a simple domain using CRC cards
- Infer database structure from domain structure
  
**Process:** 

#### CRC stands for class-responsibility-collaborator  

- Class - collection of objects
- Responsibilities - what class will/can do or knows.
- Collaborators -  classes that need other class to complete their responsibilities. 

- User stories:

```
As a coach
So I can get to know all students
I want to see a list of students' names

I want to filter the list of students by cohort name

I want each student name's name to link to the URL of a picture of the student

I want to tag a student with many named tags
```

- CRC Card (Class, Responsabilities, Collaborators).

Class: Student | |
:--- | :--- 
Responsibilities: |	Collaborators:
name | 
profile_url |

Class: Cohort | |
:--- | :--- 
Responsibilities: |	Collaborators:
start_day |	student
demo_day |	

Class: Reflect | |
:--- | :--- 
Responsibilities: |	Collaborators:
rate |	student
average |	

Class: Tag | |
:--- | :--- 
Responsibilities: |	Collaborators:
tag | 	student
filter |

- Student DB table

table: Student | | | | | |
:--- | :--- | :--- | :--- | :---
id | name | profile_url | tag_id | cohort_id | reflect_id
1 |	"name" |	"url" |	1 |	1 |	1 
2 |	"name" |	"url" |	1 |	1 |	1
					
- Cohort database table

table: Cohort | | |
:--- | :--- | :---
id | start_day | demo_day			
1 |	"day" |	"day"			
					
- Reflection DB table

table: Reflect | |
:--- | :--- 
id | rate
1 | int				
					
- Tag DB table 

table: Tag | |
:--- | :--- 
id | tag
1 | "tag"				
					
                    
**What I've Learned:**

>**Normalisation:** process where we take a table structure with repetition on it and we create new structures to avoid this repetitions. This way any change is made only in one place and automatically update everywhere else.

## Afternoon Challenges  

*Practice building simple Web-app.*  
[**"Daily Diary Application"**](https://github.com/EdAncerys/daily-diary-app)

**Process:**

Mini project exploring how databases work.

## Description

I enjoy keeping a journal, and I want to store this online in my very own 'Daily Diary' application.

As a busy coach I'm a bit short on time, so I've provided user stories below so you can build one for me. Your challenge is to build a 'Daily Diary' application that uses Sinatra together with a PostgreSQL to store diary entries, and has a browser-based user interface.

## User Stories

### Must Have

```
As a user
So that I can keep a daily diary
I want to be able to add a new Diary Entry
```

```
As a user
So that I can identify my entry in future
I want to give each Diary Entry a title
```

```
As a user
So that I can browse my previous entries
I want to see a list of Diary Entry Titles
```

```
As a user
So that I can read my previous entries
I want to click on a title to see the full Diary Entry
```

### Should Have

```
As a user
So that I can correct an error
I want to be able to edit the Diary Entry
```

```
As a user
So that I can keep my diary tidy
I want to be able to delete a Diary Entry
```

```
As a user
So that I can reflect on a previous diary entry
I want to be able add a Comment to a Diary Entry
```

```
As a user
So that I can see my past reflections
I want to see associated Comments when viewing a Diary Entry
```

### Could Have

```
As a user
So that I can make entries easier to browse
I want to be able to add Tags to an Entry
```

```
As a user
So that I can see different types of entry
I want to be able to filter Diary Entries by Tag
```

**Domain Model:**

Diary | User 
:--- | :---
 | @username
 | @email  
 | @password 
 | 
#create | #valid_log_in?
#all |
#find | 
#delete | 
#edit | 

**Databases Plan:**

- Table diary:

|  id  |    title   | body | post_time | users_id  |
|:------|:-----------|:-----------|:-----------|:------------
|  1   |  'Diary One'  |  'Diary One body' | 13:25  |     1     
|  2   |  'Diary Two'  |  'Diary Two body' | 17:05  |     1     

- Table Users:

|  id  |    name   |      email      |  password  
|:-----|:----------|:----------------|:-----------
|  1   |  'Frodo'  | 'frodo@eamil.com' | 'password' 



**Views Plan:**
```
get '/diary'            -->  display diary.erb (link to link to log_in - peep list)
get 'diary/sign_up'     --> diaplays sign_up.erb
post 'diary/sign_up'    --> saves data to DB and redirects to 'diary/user'
get 'diary/sign_in'     --> displays sign_in.erb
post 'diary/sign_in'    --> validates data and redirects to 'display/user'
get 'diary/user'        --> displays form to add diary to DB
post 'diary/add_diary'  --> saves diary to DB redirects to 'diary/list'
get 'diary/list'        --> displays all TITLE diaries 
get 'diary/list:id'     --> displays diary selected


```

**What I've Learned:**

> Working with **test and production databases** is a must in order to take TTD approach in building the application. 

> Test development database can be reset every time before tests by running script in `spec_helper.rb` file.

## Weekend Challenge

**Chitter Challenge:** Full path to the project on [GitHub](https://github.com/EdAncerys/chitter-challenge)

### Chitter App Challenge

We are going to write a small Twitter clone that will allow the users to post messages to a public stream.

### CRS Cards

### Domain model

Chitter | Peep | User
:--- | :--- | :---
#chitter_post | #peep_time | #user_sign_up
#chitter_all |  | #user_log_in
#chitter_delete |  | #user_log_out

### Database model 

chitter_user

id | name | email | password  
:--- | :--- | :--- | :---
1 | "Frodo" | "user-email@email.com" | "password"

chitter_peep

id | peep | peep_time | user_id
:--- | :--- | :--- | :---
1 | "peep" | "peep_time" | 1



**Views Plan:**
```
get '/'                 --> display sign-up and log-in path
get '/chitter'          -->  display peeps and chitter main page (links to other pages)
get 'user/sign_up'      --> diaplays sign_up.erb 
post 'user/sign_up'     --> saves data to DB and redirects to '/chitter'
get 'user/log-in'       --> displays sign_in.erb
get 'chitter/log-in'    --> validates data and redirects to 'display/user'
post 'chitter-post'      --> post peep and saves to DB redirects to '/chitter'
post 'chitter/delete/:id'  --> deletes peep from DB and redirects to '/chitter'
get 'chitter-sort'      --> displays all peeps in reverse order 
get 'chitter/log-out'   --> logs out user and destroy `session`

```

## Instructions to set up Database:
- Connect to psql
- Create the database using the psql command `CREATE DATABASE chitter_app;`
- Connect to the database using the pqsl command `\c chitter_app;`
- Run the query we have saved in the file 01_create_diary_table.sql
- Run the query we have saved in the file 02_create_user_chitter_table.sql

### create a test environment
- Create the database using the psql command `CREATE DATABASE chitter_app_test;`
- Connect to the database using the pqsl command `\c chitter_app_test;`
- Run the query we have saved in the file 01_create_diary_table.sql
- Run the query we have saved in the file 02_create_user_chitter_table.sql

Technical Approach:
-----

Integration of `PG` gem and `SQL` queries. 

Notes on functionality:
------

* You don't have to be logged in to see the peeps.
* Makers sign up to chitter with their email, password, name and a username (e.g. frodo@makersacademy.com, password123, Sam Morgan).
* The username and email are unique.
* Peeps (posts to chitter) have the name of the maker and their user handle.

Bonus:
-----

If you have time you can implement the following:

* In order to start a conversation as a maker I want to reply to a peep from another maker.

And/Or:

* Work on the CSS to make it look good.

**Features:**

## User Stories/Features

```

STRAIGHT UP

As a Maker
So that I can let people know what I am doing  
I want to post a message (peep) to chitter

As a maker
So that I can see what others are saying  
I want to see all peeps in reverse chronological order

As a Maker
So that I can better appreciate the context of a peep
I want to see the time at which it was made

As a Maker
So that I can post messages on Chitter as me
I want to sign up for Chitter

HARDER

As a Maker
So that only I can post messages on Chitter as me
I want to log in to Chitter

As a Maker
So that I can avoid others posting messages on Chitter as me
I want to log out of Chitter

ADVANCED

As a Maker
So that I can stay constantly tapped in to the shouty box of Chitter
I want to receive an email if I am tagged in a Peep
```

# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?
- I felt that I did understood main concepts and goals for a week. One thing to point out - through out a week I tend to rush and force through the challenges without deeply understanding them. That makes rest of the week dragging me with basic understanding of the concepts. Weekends **AGAIN** is usually the time to recap/reflect and understand all the concepts and goals raised. 

### What things do you still need to work through?
- Pause on weekly goals through out the week, make sure you understand them as you go. 
- DB relationships between data and dependencies on each other.

### What would you change/improve to keep moving forward?
##### Technical: 
- Break down main goals and understand them through out the week as I go.

##### Personal:

- Stick to the routine and make sure to get regular breaks.

<br>


