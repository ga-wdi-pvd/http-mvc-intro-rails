# Intro to MVC and Rails

## Learning Objectives

- Describe the role of a web framework such as Rails
- Describe the components of an MVC application
- Diagram & annotate the lifecycle of an HTTP request in Ruby on Rails
- Explain how Ruby on Rails implements MVC
- List the most common folders in a Rails application and describe their purpose
- Explain how Convention over Configuration relates to Ruby on Rails
- Describe how to read understand and fix errors in a Rails application

## Framing (10 min)

As our applications get more complicated, we need ways to help manage the
*complexity* and *size*. We have lots of tools to help us do this.

<details>
<summary>What are some some of these tools?</summary>

* Breaking code into separate files
  * Each file has code related to one 'job'
* OOP - model our program as objects with data and behavior (properties and methods)

</details>

<br>
There are other tools we have as programmers. One tool is the idea of a **design
pattern**. A design pattern is a higher-level pattern that shapes how we build
and structure our code.

One such pattern for designing applications is MVC, which stands for **Model,
View, Controller**.

We're going to talk about MVC, because that's the pattern that Rails implements.

If you've seen Sinatra, you've already seen a pattern that is very close to MVC,
but not quite. If you've seen ActiveRecord, then you've already seen a library
that helps you build *models*.

MVC can be used in lots of types of applications... there are MVC-style
frameworks for building native desktop apps (like Microsoft's ASP.net or Cocoa
for Mac), mobile apps (iOS and Android toolkits can follow MVC) or other web
frameworks like Django (in Python) or CakePHP.

MVC is *not* the only design pattern for applications, we'll see somewhat
related, but different patterns in JS frameworks like Angular or Backbone (MV*).

This lesson will not include writing much (if any) code at all. We are going to
take a high-level theoretical approach. It's extremely important to understand
the underlying concepts before jumping into such a heavy duty framework such as
Rails.

## What is MVC?

MVC is all about separating your code into separate sections:

* **Models** - which represent the data in your application, and help you save, load,
update, validate, etc.
* **Views** - which describe how to present your data in a way that the user can
see and interact with.
* **Controllers** - which are responsible for responding to user requests, and
contain the code for implementing features, using models and views to help them
get the job done.

## Rails and MVC (10)

Because Rails is for Web Apps, there's one additional component it adds to MVC,
a router. Thus we sometimes say that Rails is built around rMVC - router, models,
views and controller.

![rMVC](http://i.stack.imgur.com/Sf2OQ.png)

Life Cycle of the request/response in Rails:

1. A user of our web application submits a request to our application's server.
It can come in a myriad of ways. Maybe someone typing in a URL and hitting enter
or maybe a user submitting a form on our application.

2. The request hits the router of the application.

3. The application then either doesn't recognize the route (error) or it does
recognize it (route) and sends it to a controller.

4. Once the controller gets the request, it performs any necessary actions. This
might include fetching, updating, deleting, or creating information using one
or more models.

5. Once the controller has performed any actions / retrieved any inforamation
from the model(s), it uses a view to *render* an HTML page.

6. The rendered view is then sent back to the client as a response.

## Break (10 min)

## We Do: In person MVC (30 min)

## Rails Apps

### Convention Over Configuration in Rails

So what is Rails? Rails is a powerful, full-featured web framework that follows
relatively strict conventions in order to streamline our web development
process.

> It is designed to make programming web applications easier by making
assumptions about what every developer needs to get started. It makes the
assumption that there is a "best" way to do things, and it's designed to
encourage that way - and in some cases to discourage alternatives. - Ruby on
Rails guide

> Rails is a framework with lots of rules/conventions. Pay attention to the
conventions you'll need to follow for Rails throughout the week.

### Rails Walkthrough (5 min)

Let's walk through a Rails App to get comfortable with it's file structures and
identify where we will be configuring the all of the concepts we discussed
above!  Today, we'll be taking a look at [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution)!
(yes, use the solution branch!)

As we go through the app and code, you will notice how everything is abstracted
into individual files and directories. Why?

- Separation of concerns
- Readability
- Convention over configuration (rails conventions)

## You Do: Explore the folders (5 min)

Instructions:

* Clone (no need to fork) [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution)

* Students should open up the ```app``` folder and explore the code on their own.

* Note anything that reminds you of our in person exercise!

### What does a Rails App look like? (5 min)

* Note: when we first generated Tunr, we ran the following command:

**DO NOT run this command during this lesson**

```bash
$ rails new tunr -d postgresql
```

As soon as we generate a Rails app, you can see there are already many folders
and files generated from just the one command.

![Rails folder structure](images/rails_folders.png)

It can be quite daunting at first. It'll take some getting used to, but more
importantly, you're already familiar with a lot of the stuff in rails we'll be
using. Additionally, you can ignore a lot of the other stuff until you need to
incorporate some weird gem/dependency. So we started learning about *"convention
over configuration"* during the class for Active Record.

 As we scale to a Rails
size application, We can quickly see the need for conventions in such a massive
framework. Specifically for folder and file structure, Rails can be quite
particular about how we name things. Throughout this week we'll be going through
a bunch of different conventions we need to follow.

The first folder we'll talk about is the `app` folder:

![Rails app folder](images/rails_app.png)

This folder is the the most important folder in your entire application. It'll
have pretty much most of the programs functionality resting in it.

- `assets` - This will be where all of your CSS, JS, and image files belong.
- `controllers` - This folder will contain all controllers.(ST - WG) What do controllers do for us?
- `helpers` - This is where you can define any helper methods for your application
- `mailers` - Won't be covering mailers in the scope of this class. Mailers are utilized to send and receive email within a rails application. But it's pretty simple, if you want to learn more about it. You can look [here](http://guides.rubyonrails.org/action_mailer_basics.html)
- `models` - this folder will contain our AR models.
- `views` - This folder contains all of the views in this application.

> These folders are easily the most important part of your application. Not to
say the other parts aren't.

The `bin` folder contains binstubs. Not going over this in the scope of this
class, but basically they're used as wrappers around ruby gem executables(like
pry) to be used in lieu of `bundle exec`

The `config` is another folder that's pretty important. The file you'll most be
visiting is `routes.rb` This is the router in rMVC.

The `db` folder is one you'll be working in for a bit of time as well. This
contains the seed file but additionally it will also contain your migrations
which you'll be going over in the next class.

In the main directory there are a couple of files your familiar with, the
`Gemfile` and `Gemfile.lock`

### Starting a Rails Server (5 min)

Let's go ahead and look at the final application before we dive into the code.

>if you want to follow along, clone it down and checkout the solution branch

In my console, I'm going to run the following commands:

- this loads & sets up the local dependencies
```bash
$ bundle install
```

- this is similar to `psql dbcreate <database name>` (plus more)
```bash
$ rake db:create
```

- this command sets up the schema (plus more)
```bash
$ rake db:migrate
```

- this command runs the seeds file to seed the database
```bash
$ rake db:seed
```

- this command starts the server
```bash
$ rails s
```

We should see something like:

```
=> Booting WEBrick
=> Rails 4.2.6 application starting in development on http://localhost:3000
=> Run `rails server -h` for more startup options
=> Ctrl-C to shutdown server
[2016-03-09 09:02:00] INFO  WEBrick 1.3.1
[2016-03-09 09:02:00] INFO  ruby 2.2.3 (2015-08-18) [x86_64-darwin15]
[2016-03-09 09:02:00] INFO  WEBrick::HTTPServer#start: pid=97614 port=3000
```

Let's focus on this particular line:
`=> Rails 4.2.6 application starting in development on http://localhost:3000`

And enter `http://localhost:3000` in our browser.

>The number `3000` is the port number. This is the default port number in a Rails Application.

## Break (10 min)


### Walkthrough of Tunr (20 min)

Let's make a few requests in our browser, and trace the path of the code runs
as a result of each request:

- `GET` artist info
- `PUT` changed info on the artist page
- `POST` a new artist
- `DELETE` an artist

### Questions (10 min)

#### Routes

- Where do we configure our routes in a Rails Application?
- What is the syntax for writing routes in a Rails App?
- Why are we including a symbol again in `artists/:id` in our path?
- What does `artists#index` and `shows#index` referring to?

<details>
<summary>
Answers
</summary>
<br>
- config/routes.rb
<br>
- `GET` request example: `get "artists" => "artists#index"``
<br>
- Can dynamically change the id of artist and grab those params as needed in our application
<br>
- On the right side of the hash rocket `"artists#index"` its specifying the ***controller*** and an ***action*** within that controller. In this case, when a user of our site accesses the `artists` path(`http://localhost:3000/artists`), that request will be sent to the artists controller and execute the index action inside that controller.
<br>
</details>

#### Views
- What is this `index.html.erb` file type?
- Does it matter what we name our views, for example, does it matter if it's plural or singular?
- What is the layouts directory used for?

<details>
<summary>
Answers
</summary>
<br>
- html.erb is an html file type that allows for in line ruby code. As we will see, developers use embedded ruby tags such as ```<% %>```
<br>
- Yes! it does matter that we make these folder names plural. Rails convention says to make the folders in the views match up with the controllers
<br>
- This creates the base layout of your page. If you have a nav bar that should remain throughout your app, the layout is the place to be!
It also allows you to link script and css files in one place.
<br>
</details>

#### Models
- Where does the model get used?
- Where have we seen models like this before?
- What does has_many and belongs_to mean?

<details>
<summary>
Answers
</summary>
<br>
- corresponding controllers
<br>
- These are ActiveRecord models!
<br>
- These define the relationships between models. In the case of Tunr, we have a simple one-many relationship: one artist has many songs
<br>
</details>

## Reading Rails Errors
One of the best part about Rails is the errors! What?

Rails provides detailed, and understandable, errors that allow you to take the
necessary steps to build a working app. We won't go too deep into them during
this class, but you will get plenty of exposure during the upcoming lessons!
Lets go into our browser and go to `http://localhost:3000/mispelledartists` and
we'll see:

![no route error](images/no_route.png)

## Closing (5 min)
* Review LO's

* Let's take a look at another real world example: [garnet](https://github.com/ga-dc/garnet)!
> Note, this app has taken MONTHS and 10 devs to build. Don't freak out!

## Additional Resources
- [Rails Documentation](http://api.rubyonrails.org/)
- [Rails Github](https://github.com/rails/rails)
