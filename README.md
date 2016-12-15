# Hello Rails

## Learning Objectives

- Describe the role of a web framework such as Rails
- Describe the components of an MVC application
- Diagram & annotate the lifecycle of an HTTP request in Ruby on Rails
- Explain how Ruby on Rails implements MVC
- Create a Rails application that displays "Hello Rails!"
- List the most common folders in a Rails application and describe their purpose
- Explain how Convention over Configuration relates to Ruby on Rails
- Describe how to read, understand and fix errors in a Rails application

## Framing (5 minutes / 0:05)

What do  Airbnb, Basecamp, Disney, GitHub, Hulu, Kickstarter, Shopify, Twitter, and the Yellow Pages all have in common? They were built on the Ruby on Rails framework. Sure, there are many other systems in play with massive sites such as these, but they all, at one time or another, were based on the Ruby on Rails framework.

"Rails is a web-application framework that includes everything needed to create database-backed web applications according to the Model-View-Controller (MVC) pattern." -[Rails Docs](http://api.rubyonrails.org/)

Today we are not going to get into the nuances and gritty details of Rails. Instead, we will give you a brief introduction into the back-end framework. In [future lessons](https://github.com/ga-wdi-pvd/rails_features_CRD), we are going to get into the full power of Rails, including the ability to CRUD with the best of 'em. By learning the "what" and "why" of Rails first, we are laying the foundation for deeper understanding when you dive into full-fledged Rails apps later. Remember, you are learning the same system that powers some of the largest sites on the web.

## Why Rails? (10 minutes / 0:15)
What makes Rails so special? Why has it become so popular as a web development framework? 

- One of the reasons is that it is completely open source. 

  -Check out the [source code](https://github.com/rails/rails) on Github.
    - what can you tell me about the Rails project, by looking at its github page? 
      - open source stats:
       - 60,000 + commits
       - 3000 + contributors 
       - 13,000 + forks (!)
    - current version…
      - current version: Rails 5
      - Do you think you are going to work with multiple versions of Rails? In the real world it takes years for companies to go from rails 3 to 4, and 4 to 5. You should be familiar with how to use different versions. Tools like [Ruby Version Manager (or RVM)](https://rvm.io/) can help with that

    - Are there outstanding issues yet to be merged in Pull Requests? What do these pull requests represent?

A few more reasons that people use Rails:

- It is written with Ruby, which is more fun to work with than Java, ASP.net, and PHP. Writing in Ruby makes developers happy. Happy developers write good code.  Check out this [history of web frameworks timeline](https://github.com/mraible/history-of-web-frameworks-timeline) to see what Rails was competing with back in 2004 - 2005. 

- Rails is expressive. It uses something called a DSL (Domain Specific Language) built on top of Ruby that allows very readable code, such as associations which we've seen: `has_many` and `belongs_to`. And validations are a snap: What do you think `validates_presence_of :title` does when placed in the `song.rb` class of `Tunr`?

- Rails is opinionated. It's configured out of the box for web apps to "just work". This is great for many developers, and if you want to customize it, you can do that too, because it's all open source. And free.

- Maturity - it's been around long enough to have the major kinks and security issues worked out.

- Community - there is a large, dedicated community that is ready to help developers when we get in a bind.

- Ruby Gems - there is a large colleciton of mature Ruby libraries we can plug into our Rails apps, which allows us to do more and write less. Need some functionality? There's likely a ruby gem for that. If not, write your own!

But of course, Rails is not right for every project by any means. It is not a silver bullet to solve all problems and make millions in Silicon Valley. Smaller projects may just need something like Sinatra, or you could write plain ruby and include a few specific ruby gems to round out your web app. Just remember not to reinvent the wheel.

> NOTE: Rails has been around since 2004, and it is a BIG project. It will take you YEARS to get to know all of it, BUT you only need to know a handful of commands to get started. Do not get discouraged by the amount of brand new stuff in a Rails project and in the Rails ecosystem on the web. By the end of this lesson, you are NOT expected to know the meaning behind each file and folder. All we want to focus on during this lesson is to get a feel for what Rails is all about and make comparisons between it and Sinatra. We'll get plenty of practice with more Rails features and capabilities in future lessons.

This lesson will not include writing much - if any - code at all. We are going to
take a high-level theoretical approach. It's extremely important to understand
the underlying concepts before jumping into such a heavy duty framework such as
Rails.

First, we are going to talk more about the design and architecture of a Rails application, and the pattern that it uses, the MVC pattern.

## What Is MVC? (10 minutes - 0:25)

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

## Rails and MVC (5 minutes / 0:30)

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

## We Do: In-Person MVC (20 minutes / 0:50)
- As a class, everyone will count off, 1-7.
- Divide students into roles as specified here:
https://github.com/ga-wdi-pvd/http-mvc-intro-rails/blob/master/exercise.md

## Hello Rails

### Convention Over Configuration in Rails (5 minutes / 0:55)

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

Rails is a framework with lots of rules/conventions. Pay attention to the conventions, and don't swim upstream! Learn the rules so that you will know how to effectively break them when the time comes :)

### Rails Walkthrough (5 minutes / 1:00)

Let's walk through a Rails App to get comfortable with its file structure and
identify where we will be configuring all of the concepts we discussed
above.

Go ahead and checkout a copy of the [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution) application, rewritten in the Rails framework:

```bash
$ git clone https://github.com/ga-wdi-exercises/tunr_rails_views_controllers.git
$ cd tunr_rails_views_controllers
$ git checkout solution
```

As we go through the app and code, you will notice how everything is abstracted
into individual files and directories. Why?

- Separation of concerns
- Readability
- Rails Conventions

## You Do: Scavenger Hunt (15 minutes / 1:15)

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

> Make notes about anything else that reminds you of Sinatra, and anything that you are curious about.

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

## Break! (10 minutes / 1:25)

### What Does a Rails App Look Like? (15 minutes / 1:40)

#### You Do: Create your app

Let's create our own Rails app:

```bash
$ cd my_ga_projects_directory
$ rails new hello_rails
$ cd hello_rails
```
#### Questions and a Look into Common Folders

What happened during this generate command?
- made a bunch of files
- `bundle install`
- was a database created?

As soon as we generate a Rails app, you can see there are already many folders
and files generated from just the one command (`rails new`)

![Rails folder structure](images/rails_folders.png)

While all these files may be daunting at first, you're already familiar with many of these components from your work with Sinatra. 

As we scale to a Rails size application, we can quickly see the need for conventions in such a massive
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

### Setup Commands (You Do) (10 minutes / 1:50)

> 5 minutes exercise. 5 minutes review.

The following are common commands that you will encounter when working with Rails applications. Your task is to run these in order and, based on the context clues (e.g., terminal output), figure out what they're doing. You answers don't need to be technical - keep it high level.

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
  * `bundle exec` makes sure you are executing the correct command in the context of your rails app. The presence of "binstubs" in the `yourRailsApp/bin` directory are wrappers for these commands and allow you to safely just run commands like `rails s` without prefixing `bundle exec`

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

### HTTP Request-Response Cycle (I do - Draw on Board) (5 minutes / 1:55)

Using our knowledge of the MVC request-response cycle and the files/folders we discovered during the scavenger hunt exercise, let's try following the path of an HTTP request through a Rails application. 

Remember, HTTP is a protocol - a system of rules - that determines how web pages get sent from one place to another. (Hyper Text Transfer Protocol). Among other things, http it defines the format of the messages passed between HTTP clients and an HTTP server.  Since the web is a *service*, it works through a combination of *clients* (which make requests) and *servers* (which receive requests).

Let's GET the homepage.
- What does the request-repsonse cycle look like for this request? What files does it touch? How do we know?

Next let's talk about routes

#### Routes (5 minutes / 1:55)

1. Where do we configure our routes in a Rails Application?
- What is the syntax for writing routes in a Rails App?
2. How do we change the route to our homepage?
3. What does this route mean?
  - `get "artists" => "artists#index"`
  - `post "artists/update" => "artists#update"`
4. How can we route to a dynamic page, such as `artists/4` (or `artists/10020`)?

<details>
  <summary><strong>Answers</strong></summary>

  > 1. config/routes.rb
  >
  > 2. Uncomment `root welcome#index` to point to our homepage. Note that you need to create this `welcome` controller with an action, `index`, for this to work correctly.
  >
  > 3. Routing examples
     - The first route: `GET` request example: `get "artists" => "artists#index"`` says that when a request comes into the "artists" path that is a GET request, go to the "`artists` controller `index` action"
     - The 2nd route: `POST` request example: `post "artists/update" => "artists#update"` says that when a request comes into the "artists/update" path and is a POST request, go to the "`artists` controller `update` action"
  > 
  > 4. Can dynamically change the id of artist and grab those params as needed in our application by using a symbol in the route: `get "artists/:id" => "artists#show"`, which says when a GET request comes into the path "artists" with anything after it (artists/4 or artists/10020), it routes to the controller `artists` with action `show`, and a param of `id` is available to our controller in the `params` hash (`params[:id]`)

</details>

In summary, the route is comprised of two parts: a path that the request is sent to, and a controller action that we route that request to. 

Take a look at `get 'dog/bark' => 'dogs#make_dog_bark'`. 

On the left side of the route declaration, we specify the HTTP verb and the path, , and on the right side of the hash rocket, we are specifying the ***controller*** and an ***action*** within that controller. In this case, when a user of our site accesses the `dog/bark` path(`http://localhost:3000/dog/bark`), that request will be sent to the `dogs.rb` controller and execute the `make_dog_bark` action inside that controller.

The routes file can be pretty complex, as it allows you to customize every part of incoming requests and outgoing responses. You will definetly want to have the [Rails Guide for Routing](http://guides.rubyonrails.org/routing.html) open for your first few attempts at writing routes.

#### Views (You do) (5 minutes / 2:00)

1. Let's create a view file, called `index.html.erb` within a folder called `welcome`. What is this `index.html.erb` file type?
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

#### Hello Rails! (You do)

Now we know how to change our home page route, let's point our homepage to a custom controller and action:
Steps:
- create (or go to) the `welcome` controller with the `index` action
- add text `<h1>Hello Rails!</h1>` to the `welcome/index.html.erb` view
- point your `/` route (the root of your application) to your new page
- fire up your web server with `rails s`
- visit your home page
- pat yourself on the back.

#### Models (I do)

Let's go back to our Tunr application and look at the models already set up for us

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

To demonstrate, let's visit `http://localhost:3000/somethingmissing` in the browser. We should see...

![no route error](images/no_route.png)

## Bonus Option 1 (Hard!): POST and say Hello

Let's try to POST to a new route, "hello". For this exercise, we are going to rely on error-driven development. Write a piece of code, see what error is output, then fix up our code to get to the next error.

- One way to simulate a POST, which usually comes from a form submission, is via `curl`:
`curl -d "user=Danny" http://localhost:3000/hello
- What error did we receive?
  - No route
  - let's fix this up...
    - add the route `post 'hello' => 'welcome#hello'`
- Next what error did we receive?
  - uninitialized constant WelcomeController
  - add a controller, WelcomeController
- Fix up the next error
- The final error deals with security. It turns out that Rails has built in security features so that POSTs can only come in when the app developer as specifically allowed for them. This resource may help you through this security feature when POSTing via `curl`: http://api.rubyonrails.org/classes/ActionController/RequestForgeryProtection.html
- If you are able to POST to hello and get a response, edit your "hello" action to return `hello, <%=user%>!`
- You may want to turn off rendering a layout for this controller action.

## Bonus Option 2:
- Fork, clone and install Garnet so it runs on your local machine: [garnet](https://github.com/ga-dc/garnet)!

## Closing (5 minutes / 1:50)

* Review learning objectives
* Prepare for future lessons

## Additional Resources
- [Rails Documentation](http://api.rubyonrails.org/)
- [Rails Github](https://github.com/rails/rails)

## Prework
 - Rails is famous for its [15 minute blog video](https://www.youtube.com/watch?v=Gzj723LkRJY) by DHH. Give the video a watch and get excited! But remember, this is from 2005 and some things have changed since then.
