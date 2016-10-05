# Intro to MVC and Rails

## Learning Objectives

- Describe the role of a web framework such as Rails
- Describe the components of an MVC application
- Diagram & annotate the lifecycle of an HTTP request in Ruby on Rails
- Explain how Ruby on Rails implements MVC
- List the most common folders in a Rails application and describe their purpose
- Explain how Convention over Configuration relates to Ruby on Rails
- Describe how to read understand and fix errors in a Rails application

## Framing (10 minutes / 0:10)

As our applications get more complicated, we need ways to help manage the
*complexity* and *size*. We have lots of tools to help us do this.

<details>
<summary><strong>What are some some of these tools?</strong></summary>

  > Breaking code into separate files. Each file has code related to one "job."
  >
  > Object-oriented design. Model our program as objects with data and behavior (properties and methods)

</details>

There are other tools we have as programmers. One tool is the idea of a **design
pattern**. A design pattern is a higher-level pattern that shapes how we build
and structure our code.

One such pattern for designing applications is MVC, which stands for **Model,
View, Controller**.

We're going to talk about MVC, because that's the pattern that Rails implements.

If you've seen Sinatra, you've already seen a pattern that is very close to MVC,
but not quite. If you've seen ActiveRecord, then you've already seen a library
that helps you build *models*.

MVC can be used in lots of types of applications. There are MVC-style
frameworks for building native desktop apps (e.g., Microsoft's ASP.net, Cocoa
for Mac), mobile apps (iOS and Android toolkits) or other web
frameworks like Django (Python) or CakePHP.

MVC is *not* the only design pattern for applications, but it's a popular one. We'll also see somewhat
related but different patterns in Javascript frameworks like Angular or Backbone.

This lesson will not include writing much - if any - code at all. We are going to
take a high-level theoretical approach. It's extremely important to understand
the underlying concepts before jumping into such a heavy duty framework such as
Rails.

## What Is MVC?

MVC is all about separating your code into separate sections...

* **Models**: they represent the data in our application and will be used to perform CRUD actions on our database
* **Views**: they describe how to present your data in a way that the user can
see in the browser
* **Controllers**: they are responsible for responding to user requests, and
contain the code for implementing features, using models and views to help them
get the job done

## Rails and MVC (10 minutes / 0:20)

Because Rails is for web apps, there's one additional component it adds to MVC:
a router. Thus we sometimes say that Rails is built around **rMVC** - a router, models,
views and controllers.

![rMVC](http://i.stack.imgur.com/Sf2OQ.png)

As a result, the request-response cycle looks like this for Rails...

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

## We Do: In person MVC (20 minutes / 0:40)

## Rails Apps

### Convention Over Configuration in Rails

So what is Rails? Rails is a powerful, full-featured web framework that follows
relatively strict conventions in order to streamline our web development
process.

> It is designed to make programming web applications easier by making
assumptions about what every developer needs to get started. It makes the
assumption that there is a "best" way to do things, and it's designed to
encourage that way - and in some cases to discourage alternatives. -- Ruby on
Rails guide

Rails is a framework with lots of rules/conventions. Pay attention to the
conventions you'll need to follow for Rails throughout the week.

### Rails Walkthrough (5 minutes / 0:45)

Let's walk through a Rails App to get comfortable with its file structure and
identify where we will be configuring the all of the concepts we discussed
above.

Today, we'll be taking a look at [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution). **Make sure to check out the solution branch.**

As we go through the app and code, you will notice how everything is abstracted
into individual files and directories. Why?

- Separation of concerns
- Readability
- Rails Conventions

## You Do: Explore the Folders (5 minutes / 0:50)

Instructions
* Clone down [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution)
* Students should open up the `app` directory and explore the code on their own.
* Note anything that reminds you of (1) our in-person exercises or (2) Sinatra.

### What does a Rails App look like? (5 minutes / 0:55)

When we first generated Tunr today, we ran the following command...

```bash
$ rails new tunr -d postgresql
```

> **Do not run this command during this lesson!**

<!-- AM: Do we ever run this command in class? We're cloning it down... -->

As soon as we generate a Rails app, you can see there are already many folders
and files generated from just the one command...

![Rails folder structure](images/rails_folders.png)

While all these files may be daunting at first, you're already familiar with many of these components from your work with Sinatra. Additionally, you can ignore a lot of the other stuff until you need to
incorporate some weird gem or dependency. So we started learning about *"convention
over configuration"* during the class for Active Record.

As we scale to a Rails size application, We can quickly see the need for conventions in such a massive
framework. Specifically for folder and file structure, Rails can be quite
particular about how we name things. Throughout this week we'll be going through
a bunch of different conventions we need to follow.

The first folder we'll talk about is the `app` folder...

![Rails app folder](images/rails_app.png)

This folder is the the most important folder in your entire application. It will contain
most of the programs functionality.

- **`assets`**: this will be where all of your CSS, JS, and image files belong.
- **`controllers`**: this folder will contain all controllers.(ST - WG) What do controllers do for us?
- **`models`**: this folder will contain our AR models.
- **`views`**: this folder contains all of the views in this application.

The `bin` folder contains binstubs. Not going over this in the scope of this
class, but basically they're used as wrappers around ruby gem executables(like
pry) to be used in lieu of `bundle exec`

The `config` is another folder that's pretty important. The file you'll most be
visiting is `routes.rb` This is the router in rMVC.

The `db` folder is one you'll be working in for a bit of time as well. This
contains the seed file but additionally it will also contain your migrations
which you'll be going over in the next class.

In the root directory of the application you will also see a `Gemfile` and, if you've run `bundle install`, `Gemfile.lock`

### Starting a Rails Server (5 minutes / 1:00)

Let's go ahead and look at the final application before we dive into the code.

In the console, let's run the following commands...

```bash
$ bundle install   # Loads and sets up the local dependencies
```

```bash
$ rake db:create   # Creates the database, equivalent to `createdb db_name`
```

```bash
$ rake db:migrate   # Sets up schema, equivalent to psql -d db_name < schema_file.sql
```

```bash
$ rake db:seed   # Runs seed file
```

```bash
$ rails s   # Starts the server
```

We should then see something like this appear in the Terminal...

```bash
=> Booting WEBrick
=> Rails 4.2.6 application starting in development on http://localhost:3000
=> Run `rails server -h` for more startup options
=> Ctrl-C to shutdown server
[2016-03-09 09:02:00] INFO  WEBrick 1.3.1
[2016-03-09 09:02:00] INFO  ruby 2.2.3 (2015-08-18) [x86_64-darwin15]
[2016-03-09 09:02:00] INFO  WEBrick::HTTPServer#start: pid=97614 port=3000
```

Let's focus on this particular line...

```bash
=> Rails 4.2.6 application starting in development on http://localhost:3000
```

`http://localhost:3000` is where we can begin interacting with our Rails application in the browser.

> `3000` is the default port number in a Rails Application, just like `4567` with Sinatra.

## Break (10 minutes / 1:10)

### Walkthrough of Tunr (20 minutes / 1:30)

Let's make a few requests in our browser, and trace the path of the code runs
as a result of each request:

- `GET` artist info
- `PUT` changed info on the artist page
- `POST` a new artist
- `DELETE` an artist

<!-- AM: Am I supposed to write the code here, or walk through already-existing code? -->
<!-- AM: Right now it seems to be the latter since we've cloned down the solution. -->

### Questions (10 minutes / 1:40)

#### Routes

1. Where do we configure our routes in a Rails Application?
- What is the syntax for writing routes in a Rails App?
- Why are we including a symbol again in `artists/:id` in our path?
- What are `artists#index` and `shows#index` referring to?

<details>
  <summary><strong>Answers</strong></summary>

  > 1. config/routes.rb
  >
  > 2. `GET` request example: `get "artists" => "artists#index"``
  >
  > 3. Can dynamically change the id of artist and grab those params as needed in our application
  >
  > 4. On the right side of the hash rocket `"artists#index"` its specifying the ***controller*** and an ***action*** within that controller. In this case, when a user of our site accesses the `artists` path(`http://localhost:3000/artists`), that request will be sent to the artists controller and execute the index action inside that controller.

</details>

#### Views

1. What is this `index.html.erb` file type?
- Does it matter what we name our views. Does it matter if it's plural or singular?
- What is the layouts directory used for?

<details>
  <summary><strong>Answers</strong></summary>

  > 1. html.erb is an html file type that allows for in line ruby code. As we will see, developers use embedded ruby tags such as ```<% %>```
  >
  > 2. Yes! it does matter that we make these folder names plural. Rails convention says to make the folders in the views match up with the controllers
  >
  > 3. This creates the base layout of your page. If you have a nav bar that should remain throughout your app, the layout is the place to be! It also allows you to link script and css files in one place.

</details>

#### Models

1. Where does the model get used?
- Where have we seen models like this before?
- What does `has_many` and `belongs_to` mean?

<details>
  <summary><strong>Answers</strong></summary>

  > 1. Corresponding controllers
  >
  > 2. These are ActiveRecord models!
  >
  > 3. These define the relationships between models. In the case of Tunr, we have a simple one-many relationship: one artist has many songs

</details>

## Reading Rails Errors

One of Rails' best features are its errors. Why?

Rails provides detailed, understandable errors that provide guidance when building an application. We won't go too deep into them during
this class, but you will get plenty of exposure during the upcoming lessons.

To demonstrate, let's visit `http://localhost:3000/mispelledartists` in the browser. We should see...

![no route error](images/no_route.png)

## Closing (5 minutes / 1:45)

* Review learning objectives
* A real world example: [garnet](https://github.com/ga-dc/garnet)!

## Additional Resources
- [Rails Documentation](http://api.rubyonrails.org/)
- [Rails Github](https://github.com/rails/rails)

# TO DOs
* Add note about what `rake` means
