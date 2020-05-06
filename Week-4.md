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

**What I've Learned:**

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
- Static method is declared with static keyword. Instance method is not with static keyword.
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

**Plan:** Pair with Marius and keep working on the afternoon challenge for the week - *"Bookmark Manager".*

**Process:**

**What I've Learned:**
