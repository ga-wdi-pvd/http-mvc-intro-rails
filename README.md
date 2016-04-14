# http-mvc-intro-rails

## Learning Objectives

- Describe the role of a web framework such as Rails
- Diagram & annotate the lifecycle of an HTTP request in Ruby on Rails
- Explain how Ruby on Rails implements MVC
- List the most common folders in a rails application and describe their purpose
- Explain how Convention over Configuration relates to Ruby on Rails
- Describe how to read understand and fix errors in a Rails application

## Framing (10 min)

Let's look at [Facebook](https://www.facebook.com/). What would be missing if Zuck only used HTML, CSS, and JS to build it?
> We'd have to create a new account every time we open the app.
> We'd have to repopulate our friend list every time we opened it.
> Our status would be lost every time we refresh the browser

So, what is a server-side application?
The generally accepted practice for building a web application is to have your server deliver your homepage and handle saving and loading persistent data, based on simple messages, from the browser

So what is Rails?
Rails is a heavy duty web server-side framework that follows relatively strict conventions in order to streamline our web development process.

> It is designed to make programming web applications easier by making assumptions about what every developer needs to get started. It makes the assumption that there is the "best" way to do things, and it's designed to encourage that way - and in some cases to discourage alternatives. - Ruby on Rails guide

> Rails is a framework with lots of rules/conventions. Pay attention to the conventions you'll need to follow for rails throughout the week.

This lesson will not include writing much (if any) code at all. We are going to take a high-level theoretical approach. It's extremely important to understand the underlying concepts before jumping into such a heavy duty framework such as Rails.

## Rails

## rMVC (10 min)

![rMVC](http://i.stack.imgur.com/Sf2OQ.png)

The design pattern that rails is built around is rMVC - router, model, view and controller.

Life Cycle of the request/response in Rails:

1. A user of our web application submits a request to our application's server. It can come in a myriad of ways. Maybe someone typing in a URL and hitting enter or maybe a user submitting a form on our application.

2. The request hits the router of the application.

3. The application then either doesn't recognize the route (error) or it does recognize it(route) and sends it to a controller.

4. Once the request hits the controller, it's then going to query the database through Active Record(the model) for the information specified in the controller.

5. Once the controller has the information from the model that it needs it sends it to the view

6. The view takes the objects from the controller and sends a response to the user.

## Break (10 min)

## We Do: In person MVC (30 min)

### Rails Walkthrough (5 min)

Let's walk through a Rails App to get comfortable with it's file structures and identify where we will be configuring the all of the concepts we discussed above! Enter [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution)! (yes, use the solution branch!)

As we go through the app and code, you will notice how everything is abstracted into individual files and directories. Why?

- Separation of concerns
- Readability
- Convention over configuration (rails conventions)

## You Do: Explore the folders (5 min)

Instructions:

* Fork and Clone [Tunr](https://github.com/ga-wdi-exercises/tunr_rails_views_controllers/tree/solution)

* Students should open up the ```app``` folder and explore the code on their own.

* Note anything that reminds you of our in person exercise!

### What does a Rails folder look like? (5 min)

As soon as we generate a Rails app, you can see there are already many folders and files generated from just the one command.

* Note: when we first generated Tunr, we ran the following command:

**DO NOT run this command during this lesson**

```bash
$ rails new tunr -d postgresql
```


![Rails folder structure](images/rails_folders.png)

It can be quite daunting at first. It'll take some getting used to, but more importantly, you're already familiar with a lot of the stuff in rails we'll be using. Additionally, you can ignore a lot of the other stuff until you need to incorporate some weird gem/dependency. So we started learning about "convention over configuration" during the class for Active Record. As we scale to a rails size application, We can quickly see the need for conventions in such a massive framework. Specifically for folder and file structure, rails can be quite particular about how we name things. Throughout this week we'll be going through a bunch of different conventions we need to follow.

The first folder we'll talk about is the `app` folder:

![Rails app folder](images/rails_app.png)

This folder is the the most important folder in your entire application. It'll have pretty much most of the programs functionality resting in it.

- `assets` - This will be where all of your CSS, JS, and image files belong.
- `controllers` - This folder will contain all controllers.(ST - WG) What do controllers do for us?
- `helpers` - This is where you can define any helper methods for your application
- `mailers` - Won't be covering mailers in the scope of this class. Mailers are utilized to send and receive email within a rails application. But it's pretty simple, if you want to learn more about it. You can look [here](http://guides.rubyonrails.org/action_mailer_basics.html)
- `models` - this folder will contain our AR models.
- `views` - This folder contains all of the views in this application.

> These folders are easily the most important part of your application. Not to say the other parts aren't.

The `bin` folder contains binstubs. Not going over this in the scope of this class, but basically they're used as wrappers around ruby gem executables(like pry) to be used in lieu of `bundle exec`

The `config` is another folder that's pretty important. The file you'll most be visiting is `routes.rb` This is the router in rMVC.

The `db` folder is one you'll be working in for a bit of time as well. This contains the seed file but additionally it will also contain your migrations which you'll be going over in the next class.

In the main directory there are a couple of files your familiar with, the `Gemfile` and `Gemfile.lock`

### Starting a Rails Server (5 min)

Let's go ahead and look at the final application before we dive into the code.
>if you want to follow along, clone it down and checkout the solution branch

In my console, I'm going to run the following command:
```bash
$ rails s
```

We should see something like:
```
=> Booting WEBrick
=> Rails 4.2.4 application starting in development on http://localhost:3000
=> Run `rails server -h` for more startup options
=> Ctrl-C to shutdown server
[2016-03-09 09:02:00] INFO  WEBrick 1.3.1
[2016-03-09 09:02:00] INFO  ruby 2.2.3 (2015-08-18) [x86_64-darwin15]
[2016-03-09 09:02:00] INFO  WEBrick::HTTPServer#start: pid=97614 port=3000
```

Let's focus on this particular line:
`=> Rails 4.2.4 application starting in development on http://localhost:3000`

And enter `http://localhost:3000` in our browser.

>The number `3000` is the port number. This is the default port number in a Rails Application.

Note that this isn't a server anyone else can see, but it's still a server.

(ST-WG) Do you think that the developers of facebook created/updated the facebook application right on https://www.facebook.com? Were all the changes/updates tested on that server? I hope not!

We need a way to develop in our own environment before we just put it on the web. As such, we're going to use our computers as local servers to host our applications until we move it to a production domain. In this way we can test/write code freely in our development environment.

## Break (10 min)

### Tunr (20 min)

- Let's GET artist info
- PUT changed info on the artist page
- POST a new artist
- DELETE an artist

### Questions (10 min)

#### Routes

- Where do we configure our routes in a Rails Application?
- What is the syntax for writing routes in a Rails App?
- Why are we including a symbol again in `artists/:id` in our path?
- What does `artists#index` and `shows#index` referring to?

>Answers
- config/routes.rb
- `GET` request example: `get "artists" => "artists#index"``
- Can dynamically change the id of artist and grab those params as needed in our application
- On the right side of the hash rocket `"artists#index"` its specifying the ***controller*** and an ***action*** within that controller. In this case, when a user of our site accesses the `artists` path(`http://localhost:3000/artists`), that request will be sent to the artists controller and execute the index action inside that controller.

#### Views
- What is this `index.html.erb` file type?
- Does it matter what we name our views, for example, does it matter if it's plural or singular?
- What is the layouts directory used for?

>Answers
- html.erb is an html file type that allows for in line ruby code. As we will see, developers use embedded ruby tags such as ```<% %>```
- Yes! it does matter that we make these folder names plural. Rails convention says to make the folders in the views match up with the controllers
- This creates the base layout of your page. If you have a nav bar that should remain throughout your app, the layout is the place to be!
It also allows you to link script and css files in one place.

#### Models
- Where does the model get used?
- Where have we seen models like this before?
- What does has_many and belongs_to mean?

>Answers
- corresponding controllers
- These are ActiveRecord models!
- These define the relationships between models. In the case of Tunr, we have a simple one-many relationship: one artist has many songs

## Error Driven Development
One of the best part about Rails is the errors! What?

Rails provides detailed, and understandable, errors that allow you to take the necessary steps to build a working app. We won't go too deep into them during this class, but you will get plenty of exposure during the upcoming lessons!
Lets go into our browser and go to `http://localhost:3000/mispelledartists` and we'll see:

![no route error](images/no_route.png)

## Closing (5 min)
* Review LO's

* Let's take a look at another real world example: [garnet](https://github.com/ga-dc/garnet)!
> Note, this app has taken MONTHS and 10 devs to build. Don't freak out!

## Additional Resources
- [Rails Documentation](http://api.rubyonrails.org/)
- [Rails Github](https://github.com/rails/rails)
