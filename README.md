# Intro to Ruby on Rails

## Learning Objectives

- Describe the role of a web framework such as Rails
- Describe the components of an MVC application
- Diagram & annotate the lifecycle of an HTTP request in Ruby on Rails
- Explain how Ruby on Rails implements MVC
- List the most common folders in a Rails application and describe their purpose
- Explain how Convention over Configuration relates to Ruby on Rails
- Describe how to read, understand and fix errors in a Rails application

## Framing (10 minutes / 0:10)

What do  Airbnb, Basecamp, Disney, GitHub, Hulu, Kickstarter, Shopify, Twitter, and the Yellow Pages all have in common? They were built on the Ruby on Rails framework.

RoR is a rapid web application development framework, designed to get you up and running quickly. It was made famous by the 15 minute blog video from creator David Heinnemair Hanson.

Today we are not going to get into the nuances and gritty details of Rails. Insead, we will give you a brief introduction into the back-end framework. In future lessons, we are going to get into the full power of Rails, including the ability to quickly get a web application up and running, complete with CRUD capability. By getting familiar with the Rails framework nd design choices, you are learning the same system that powers some of the largest sites on the web.

## Why Rails?
What makes Rails so special? Why has it become so popular as a web development framework? One of the reasons is that it is completely open source

Check out the [source code](https://github.com/rails/rails) on Github.
  - what can you tell me about the Rails project, by looking at its github page? 
    - open source stats…
      - 60,000 + commits
      - 3000 + contributors 
      - 13,000 + forks (!)
    - current version…
      - current version: Rails 5
      - Do you think you are going to work with multiple versions of Rails? In the real world it takes years for companies to go from rails 3 to 4, and 4 to 5. You should be familiar with how to use different versions. Tools like [Ruby Version Manager (or RVM)](https://rvm.io/) can help with that

    - Are there outstanding issues yet to be merged in Pull Requests? What do these pull requests represent?
  - created by DHH and 37 Signals

Rails is a BIG project. It will take you YEARS to get to know all of it, BUT you only need to know a handful of commands to get started. Rails is famous for its [15 minute blog video](https://www.youtube.com/watch?v=Gzj723LkRJY) by DHH

> NOTE: Do not get discouraged by the amount of brand new stuff in a Rails project and in the Rails ecosystem on the web. By the end of this lesson, you are NOT expected to know the meaning behind each file and folder. All we want to focus on during this lesson is to get a feel for what Rails is all about and make comparisons between it and Sinatra. We'll get into the nitty-gritty of Rails in subsequent lessons.

This lesson will not include writing much - if any - code at all. We are going to
take a high-level theoretical approach. It's extremely important to understand
the underlying concepts before jumping into such a heavy duty framework such as
Rails.

First, we are going to talk more about the design and architecture of a Rails application, and the pattern that it uses, the MVC pattern.

## What Is MVC?

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

You've seen Sinatra so you've already seen a pattern that is very close to MVC,
but not quite. ActiveRecord has already shown you a library that helps you build *models*.

MVC can be used in lots of types of applications. There are MVC-style
frameworks for building native desktop apps (e.g., Microsoft's ASP.net, Cocoa
for Mac), mobile apps (iOS and Android toolkits) or other web
frameworks like Django (Python) or CakePHP.

MVC is *not* the only design pattern for applications, but it's a popular one. We'll also see somewhat
related but different patterns in Javascript frameworks like Angular or Backbone.

> Some others include [MVVM](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel) (Model-View-ViewModel) and [MVP](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter) (Model-View-Presenter).


MVC is all about separating your code into separate sections...

* **Models**: they represent the data in our application 
* **Views**: they describe how to present your data in a way that the user can
see in the browser
* **Controllers**: they are responsible for responding to user requests, interacting with models and loading views

## Rails and MVC (10 minutes / 0:20)

Because Rails is for web apps, there's one additional component it adds to MVC:
a router. A router connects incoming requests on the server to the application's controller. Thus we sometimes say that Rails is built around **rMVC** - a router, models,
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

  5. Once the controller has performed any actions / retrieved any information
  from the model(s), it uses a view to *render* an HTML page.

  6. The rendered view is then sent back to the client as a response.

## We Do: In-Person MVC (20 minutes / 0:40)

## Rails Apps

### Convention Over Configuration in Rails

We've used the phrase "convention over configuration" when describing how to write things in Sinatra.

<details>
  <summary><strong>What are some examples of "convention over configuration"?</strong></summary>

  * Pluralized table names (e.g., `artists`)
  * Singular, capitalized model names (e.g., `Artist`)
  * Singular, lowercase model file names (e.g., `artist.rb`)

</details>

How does this apply to Rails? Well, Rails is a powerful, full-featured web framework that follows
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
identify where we will be configuring all of the concepts we discussed
above.

Go ahead and checkout a copy of the [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution) application, rewritten in the Rails framework:

```bash
$ git clone https://github.com/ga-wdi-exercises/tunr_rails_views_controllers.git
$ cd tunr_rails_views_controllers
$ git checkout solution
(optional)
$ bundle install
```

As we go through the app and code, you will notice how everything is abstracted
into individual files and directories. Why?

- Separation of concerns
- Readability
- Rails Conventions

## You Do: Scavenger Hunt (15 minutes / 0:50)

> 10 minute exercise. 5 minutes review.

We'll talk about what all these files and folders mean in just a moment, but first, we want to give you a chance to explore.

Your job is to look through the application and find the Rails equivalents for the following, making sure to focus your search on the `app`, `db` and `config` directories...

* Schema
* Routes
* An `Artist` model
* Code that should be run when we visit the index page for artists
* The view that should be displayed when we visit the index page for artists
* `layout.erb`
* Directories for CSS and Javascript files
* `connection.rb`

> Make notes about anything else that reminds you of Sinatra.

<details>
  <summary><strong>Answers...</strong></summary>

  * Schema - `db/schema.rb`
  * Routes - `config/routes.rb`
  * An `Artist` Model - `app/models/artist.rb`
  * Artist Index Code - `app/controllers/artists_controller.rb`
  * Artist Index View - `app/views/artists/index.html.erb`
  * `layout.erb` - `app/views/layouts/application.html.erb`
  * CSS/JS Directories - `app/assets`
  * `connection.rb` - `config/database.yml`

</details>

### What Does a Rails App Look Like? (5 minutes / 0:55)

Let's create our own Rails app:

```bash
$ cd my_ga_projects_directory
$ rails new hello_rails
$ cd hello_rails
```

What happened during this generate command?
- made a bunch of files
- `bundle install`
- was a database created?

As soon as we generate a Rails app, you can see there are already many folders
and files generated from just the one command (`rails new`)

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
- **`controllers`**: this folder will contain all controllers.
- **`models`**: this folder will contain our models.
- **`views`**: this folder contains all of the views in this application.

The `bin` folder contains binstubs. Not going over this in the scope of this
class, but basically they're used as wrappers to around ruby gem executables - like
`pry` - to be used in lieu of `bundle exec`. Their purpose is to prepare the environment for the executable.

The `config` is another folder that's pretty important. The file you'll most be
visiting is `routes.rb` This is the router in rMVC.

The `db` folder is one you'll be working in for a bit of time as well. This
contains the seed file but additionally it will also contain your migrations
which you'll be going over in the next class.

In the root directory of the application you will also see a `Gemfile` and, if you've run `bundle install`, `Gemfile.lock`

### You Do: Setup Commands (10 minutes / 1:00)

> 5 minutes exercise. 5 minutes review.

The following are commands that we always run when creating and updating a Rails application. Your task is to run these in order and, based on the context clues (e.g., terminal output), figure out what they're doing. You answers don't need to be technical - keep it high level.

| Command | What does it do? |
|---------|------------------|
| `ruby -v`  | |
| `sqlite3 --version` | |
| `rails -v` | |
| `bundle install` | |
| `bundle exec rake db:drop` | |
| `bundle exec rake db:create` | |
| `bundle exec rake db:migrate` | |
| `bundle exec rake db:seed` | |
| `bundle exec rake stats`  | |  
| `bundle exec rails s` | |

> If you need some help, try running `rake -T` in the terminal...
> Why `bundle exec` before the rest of the command? Do you always need it?

#### Bonus

Figure out what exactly "Rake" is. [Its GitHub repo is a good place to start](https://github.com/ruby/rake).

<details>
  <summary><strong>Answers...</strong></summary>

  * `ruby -v` - checks your ruby version
  * `sqlite3 --version` - checks your sqlite3 version
  * -`rails -v` checks your rails version
  * `bundle install` - Loads and sets up the local dependencies
  * `rake db:create` - Creates the database, equivalent to `createdb db_name`
  * `rake db:migrate` - Sets up schema, equivalent to `psql -d db_name < schema_file.sql`. Creates the tables in the database
  * `rake db:seed` - Runs seed file. Populates the tables.
  * `rake stats` - Your project stats, including LoC
  * `rails s` - Starts the server

</details>

------

After we've done all that and run `rails s`, we should see something like this in the Terminal...

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

## Break (10 minutes / 1:15)

### You Do: Follow A Request (20 minutes / 1:35)

> 10 minutes exercise. 10 minutes review.

Using your knowledge of the MVC request-response cycle and the files/folders you discovered during the scavenger hunt exercise, try following the path of an HTTP request through a Rails application. HTTP is a protocol - a system of rules - that determines how web pages (see:'hypertext') get sent (see:'transferred') from one place to another. Among other things, it defines the format of the messages passed between HTTP clients and HTTP server.Since the web is a service, it works through a combination of clients which make requests and servers (which receive requests).

- `GET` the homepage of your app

### Questions (10 minutes / 1:45)

#### Routes

1. Where do we configure our routes in a Rails Application?
- What is the syntax for writing routes in a Rails App?
2. How do we change the route to our homepage?
3. What does this route mean?
  - `get "artists" => "artists#index"`
4. How can we route to a dynamic page, such as `artists/4`?

<details>
  <summary><strong>Answers</strong></summary>

  > 1. config/routes.rb
  >
  > 2. change `root welcome#index` to point to our homepage
  >
  > 3. `GET` request example: `get "artists" => "artists#index"``
  > 
  > 4. Can dynamically change the id of artist and grab those params as needed in our application
  >
  > 4. On the right side of the hash rocket `"artists#index"` its specifying the ***controller*** and an ***action*** within that controller. In this case, when a user of our site accesses the `artists` path(`http://localhost:3000/artists`), that request will be sent to the artists controller and execute the index action inside that controller.

</details>

#### Views

1. What is this `index.html.erb` file type?
- Does it matter what we name our views folders. Does it matter if it's plural or singular?
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
- What conventions do we see here?

<details>
  <summary><strong>Answers</strong></summary>

  > 1. Corresponding controllers
  >
  > 2. These are ActiveRecord models!
  >
  > 3. These define the relationships between models. In the case of Tunr, we have a simple one-many relationship: one artist has many songs
  >
  > 4. These model name must be capitalized.

</details>

## Reading Rails Errors

One of Rails' best features are its errors. Why?

Rails provides detailed, understandable errors that provide guidance when building an application. We won't go too deep into them during
this class, but you will get plenty of exposure during the upcoming lessons.

To demonstrate, let's visit `http://localhost:3000/mispelledartists` in the browser. We should see...

![no route error](images/no_route.png)

## Closing (5 minutes / 1:50)

* Review learning objectives
* A real world example: [garnet](https://github.com/ga-dc/garnet)!

## Additional Resources
- [Rails Documentation](http://api.rubyonrails.org/)
- [Rails Github](https://github.com/rails/rails)
