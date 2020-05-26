# Week 6 Goals

By the end of the week all developers can build tested, easy-to-change software in a team using these processes:

- Break down projects into tasks and allocate them to pairs
- Build to a specificiation (rather than challenges)
- Run stand-ups and retrospectives
- Use a branch/PR/merge git workflow
- Give and receive meaningful code review

<br>

## Project Week: Makers BnB

Work in teams to build a clone of AirBnB. Main objective is to learn how to successfully work in a teams and organise teams work flow and communication.   
MakersBnB project repository can be found by following this link [here](https://github.com/EdAncerys/MakersBnB)

## The Team

- Ed Ancerys
- Andrew Hulme
- Ellis Trickett
- Colin Muir

## Work Structure

We decided to spend first day mostly in planing the project. Set a plan for a week and agree on goals and vision so as a team we have good understanding in which direction we need to go to to achieve it.   

Right at the start of the project we set:

- User Stories
- Domain Models for MakersBnB
- Database structure.

Decided to work in pairs of two during a day, rotate every day to keep a momentum. Have morning and afternoon stand-ups as per standard. If needed to catch up on any issues on demand as needed.

## The tools
- Diagram.codes for Domain Model
- Zoom for remote pair/group work
- GitHub
- Slack for group messages

### Work flow and planning

- Turn specifications into user stories
- Decide a priority order for the user stories
- Schedule the branch merge to master times
- Design Database tables
- Create a Domain Models

### Daily Schedule Structure

- Morning meeting
  - Decide which pending tasks are the most important for the day
  - Assign tasks to every pair
- Lunck check (optional and if needed)
  - Any issues that arise during morning that the team might need a help with.
- Evening meeting
  - Recap with rest of the team over the work done at the end of the day
  - Update README.md and pending tasks
  - Merge and pull so all of us have the same files to the master
  - Reflections
  - Suggestions
  - Feedback

## The Project

As a team we spent a lot of focus on back end implementation and making sure that we have full functionality and models in a first place. UI is functional, but styling and visual appeal not up to the standards as per original AirBnB web site.

### Specifications and User Stories

## User Stories

```
- Any signed-up user can list a new space.

As a user,
So I can have an account,
I am able to sign up.

As a user,
So I can interact with the website,
I am able to log in.

As a user,
So I can create a new listing,
I am able to list a new space.
```

```
- Users can list multiple spaces.

As a user,
So I can advertise multiple spaces,
I am able to list multiple spaces.
```

```
- Users should be able to name their space, provide a short description of the space, and a price per night.

As a user,
So I can name my space,
I can give my space a name.

As a user,
So that I can advertise my space,
I can write a short description for my space.

As a user,
So that others know how much my space costs,
I can give it a price per night.
```

```
- Users should be able to offer a range of dates where their space is available.

As a user,
So I can show when the space is available,
I want to make the space available to book over a range of dates.
```

```
- Any signed-up user can request to hire any space for one night, and this should be approved by the user that owns that space.

As a user,
So that I can rent a space,
I need to be able to request the property on a certain date.

As a user,
So that I can rent my space,
I need to be able to see my requests and approve them.
```

```
- Nights for which a space has already been booked should not be available for users to book that space.

As a user,
So that a space can't be double booked,
I shouldn't be able to book a space on those dates
```


```
- Until a user has confirmed a booking request, that space can still be booked for that night.

As a user,
So that I can decide who books the space,
My space is still available to book until I have confirmed a request.
```

```
- Extras

As a user,
so i can book an ad,
I am able to log in.

As a user,
I can view rooms.
```

### Domain Model

| class | methods |
| --- | --- |
| user | @spaces |
| | .log_in	 |
| | .sign_up |

| class | methods |
| --- | --- |
| Space | @name |
| | .add_space(name, description, price, dates_available) |
| | .view_spaces |

| class | methods |
| --- | --- |
| Booking | .book_space(name, date) |
| | .view_book_space |
| | @price |

| class | methods |
| --- | --- |
| Request | .see_requests(bookings?) |
| | .approve_request |
| | .decline_request |
| | ._update_dates_available |

### Databases

`USER` table:

| field | type |
| --- | --- |
| USER ID | PRIMARY SERIAL ID |
| EMAIL | VARCHAR(200) |
| PASSWORD | VARCHAR(60) |
| USERNAME | VARCHAR(100) |
| REAL NAME | VARCHAR(100) |

`SPACE ADVERTISMENT` table:

| field | type |
| --- | --- |
| SPACE ID | PRIMARY SERIAL ID |
| USER ID (host) | VARCHAR(100) (FOREIGN KEY) |
| NAME OF SPACE | VARCHAR(100) |
| DESCRIPTION | VARCHAR(250) |
| PRICE | Integer |
| DATES AVAILABLE | VARCHAR |


`CONFIRMED BOOKING` table:

| field | type |
| --- | --- |
| ID | PRIMARY SERIAL ID |
| USER ID (guest) | VARCHAR(100) (FOREIGN KEY)  |
| SPACE ID  | (FOREIGN KEY) |
| DATE OF BOOKING | DATE |

### View Plan
```
get '/'                     -->  display index.erb (link to sign_up and sign_in - spaces list)

get '/sign_up'              -->  display sign_up.erb (sign_up form, submit button)
post '/sign_up'             -->  redirect to ./sign_in (saves data to users table in DB)

get '/sign_in'              -->  display sign_in.erb (sign in form)
post '/sign_in'             -->  redirect to ./user (authenticates and gets new user from DB)

post '/sign_out'            -->  removes current user data

get '/user'                 -->  display user.erb (link to my_bookings - link to my_spaces - space list with links to book_space - menu)

get '/my_bookings/:user_id' -->  display my_bookings.erb (list of bookings with status - link to '/user')

get '/my_spaces'            -->  display my_spaces.erb (list of my spaces - link to create_space - link to manage_spaces - link to user)

get '/my_spaces/create_space'  -->  display spaces/create.erb (create_space form, save_button, link to my_spaces)
post '/my_spaces/create_space  -->  redirect to ./my_spaces (saves space to spaces table in DB)

get '/my_spaces/manage'     -->  display space_management.erb (list of my spaces with booking requests and accept/decline options)
post '/my_spaces/manage'    -->  redirect to ./my_spaces/manage (modifies availability in spaces DB)

get '/book_space/:id'     -->  display book_space.erb (space, confirm_booking_button)
post '/book_space/:id'    -->  redirect to ./my_bookings/user (creates a new booking instance, save data into bookings DB)
```

## **What I've Learned:**

MakersBnB challenge been a positive experience and great practice to work in a bigger team. Been challenging at times and even stressful at points as to complete a project been something that everyone in a team been aiming for.

I learned that communication and good understanding of a teams feel and spirit as equally as important as experience in building projects.

Everyones input and positive attitude is crucial in order to have stress free workflow and good communication that can lead in overall better project experience and quality.

<br>


# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?
* Goals to work in a team been met. Have way better feel of what needed to complete a project and how to work in a team as well.

### What things do you still need to work through?
* Java Script and testing with Jasmine
* TDD with RSpec

### What would you change/improve moving forward?
##### Technical:

* Review and recap end of day things learned

##### Personal:

* To have more breaks dureeing the day and have limits on time spent coding.

### A pat on the back
* Manage to end the week on a positive note and in high morale.

<br>
