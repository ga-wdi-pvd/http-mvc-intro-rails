# http-mvc-intro-rails

## Learning Objectives

- Explain the role of a server-side web application
- Explain the lifecycle of an HTTP request in Ruby on Rails
- Understand the RESTful routes and how they relate to an HTTP request
- Define example RESTful routes with URL parameters
- Explain how Convention over Configuration relates to Ruby on Rails
- Explain what Ruby on Rails is and it's architectural components (rMVC)
- List the most common folders in a rails application and describe their purpose
- Describe what error driven development is, and how we might do it in Rails

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

Before we get to deep into Rails specifically, we first need to understand the underlying architectural components and the lifecycle of requests.

This lesson will not include writing much (if any) code at all. We are going to take a high-level theoretical approach. It's extremely important to understand the underlying concepts before jumping into such a heavy duty framework such as Rails.

## Request / Response

Open our browsers and type in ESPN to the URL. What's happening?
Let's identify what is the request, and what is the response?

## Intro to HTTP and REST

### HTTP (5 min)

**Hypertext Transfer Protocol** (HTTP) is a method for encoding and transporting information between a client (such as a web browser) and a web server. HTTP is the primary protocol for transmission of information across the Internet.

A server's job is to respond to HTTP requests. In order to talk about how Rails functions, we need to talk about how HTTP requests work.

Every **HTTP request** consists of a request **method** and **path**. The path is the URL to which the request is being sent. That's pretty familiar. However, your browser always sends that request in a particular way that gives the server a hint as to the "point" of the request. This "particular way" is the method.

Once the request is made, the server grabs all sorts of information and begins to build its **response**. It renders the data on a view (HTML), and then sends it back to the client to see it on the browser.

### HTTP Methods (5 min)

HTTP defines the following methods, each of which corresponds to one of the CRUD functionalities.

| Method | Crud functionality |
|---|---|
|GET| read |
|POST| create |
|PUT| update |
|DELETE| delete |

#### What's the difference at a technical level between a GET and a POST request?

There really isn't a whole lot of difference. The browser sends the request more-or-less the same way. The difference is in how the data comprising the request is "packaged".

We'll see this in greater detail later. For now, just think that, say, a GET request is sent in a plain old white envelope, while a POST request is sent in a red envelope with "ACTION REQUIRED" written on it.

### REST (5 min)

REST, or REpresentational State Transfer, is a convention for what these HTTP methods should be to standardize all the communication between browsers and servers.

Knowing REST is important because the vast majority of web developers have agreed to follow this same convention.

"GET" is one of these methods. It means the browser just wants to read (or "get") some information. When you write `get '/say_hi' do`, you're telling your server how to respond when a browser says, "Hey, I'd like to get some information from the `say_hi` path."

We make requests all the time -- especially GET requests. Everytime you go to your browser, enter a URL, and hit enter, you're actually making a GET request.

### RESTful Routes (5 min)

A **route** is a **method** plus a **path**:

**Route = Method + Path**

Each route results in an **action**.

REST provides a template for the way different paths should look:

| Method | Path | Action | Used for |
| --- | --- | --- | --- |
| GET | `/students` | Index | Read information about all students |
| POST | `/students` | Create | Create a new student |
| GET | `/students/1` | Show | Read information about the student whose ID is 1 |
| PUT | `/students/1` | Update | Update the existing student whose ID is 1 with all new content |
| DELETE | `/students/1` | Destroy | Delete the existing student whose ID is 1 |

Note that the path doesn't contain any of the words describing the CRUD functionality that will be executed. That's the method's job. **The methods(verbs) tell the server what to do with the routes**

Let's check out the [ESPN website](http://espn.go.com/mlb/team/_/name/bal). If we go to a specific team webpage, we can see this same sort of structure in the URL.

#### Path Parameters

Ideally, we would NOT want to hard code an id for each path for students. Imagine there were over 200 students in an high school class!

Thankfully we don't have to:

We can instead change `get '/students/1'` to `get '/students/:id'`

### You Do - Create routes (10 min)

Create routes for the following requests. The first one is done for you.

1. Create a new animal
  - `POST /animals`
2. Delete an animal
3. Update an existing homework assignment
4. Create a new class at GA.
5. View all students in WDI.
6. Update the info for an animal with 3 as its id.
7. Update homework submission #32 for assignment #3

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
