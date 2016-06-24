# REST

## Learning Objectives

- Explain the role of a server-side web application
- Understand the RESTful routes and how they relate to an HTTP request
- Define example RESTful routes with URL parameters

## Request / Response

Open our browsers and type ESPN into the URL and hit enter. What's happens?

Well, pretty much to our eyes as humans, we see the screen flash, maybe a loading icon appears, then we watch as a new webpage's content is loaded.  Now depending on our internet connection, loading that page could take anywhere between a split second to a few minutes, however in that flash of time, an incredible amount of communication is happening on the back end to bring us that page.

That tiny flash or flicker we see, is the only visual clue that something is changing, but in reality that timespan is the entire lifespan of what we call the **request - response lifecycle**.

Today, we are going to talk about the different components that shape how we send and receive data across the internet, and learn how we can harness these rules to build our own full stack web applications.

## Intro to HTTP and REST

### HTTP (5 min)

**Hypertext Transfer Protocol** (HTTP) is a method for encoding and transporting information between a client (such as a web browser) and a web server. HTTP is the primary protocol for transmission of information across the Internet.

A server's job is to respond to HTTP requests. In order to talk about how Rails functions, we need to talk about how HTTP requests work.

Every **HTTP request** consists of a request **method** and **path**. The path is the URL to which the request is being sent. That's pretty familiar. However, your browser always sends that request in a particular way that gives the server a hint as to the "point" of the request. This "particular way" is the method.

Once the request is made, the server grabs all sorts of information and begins to build its **response**. It renders the data on a view (HTML), and then sends it back to the client to see it on the browser.

### HTTP Methods (5 min)

In order to identify what to do with the information sent from the browser, the HTTP protocol establishes a set list of **methods** to describe the nature of the *request*, and therefore informs the server of the subsequent actions necessary to send back a *response*.

HTTP defines the following methods, each of which corresponds to one of the CRUD functionalities.

| Method | Crud functionality |
|:-------|:-------------------|
| GET    | read               |
| POST   | create             |
| PUT    | update             |
| DELETE | delete             |

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

| Method | Path          | Action  | Used for                                                       |
|:-------|:--------------|:--------|:---------------------------------------------------------------|
| GET    | `/students`   | Index   | Read information about all students                            |
| POST   | `/students`   | Create  | Create a new student                                           |
| GET    | `/students/1` | Show    | Read information about the student whose ID is 1               |
| PUT    | `/students/1` | Update  | Update the existing student whose ID is 1 with all new content |
| DELETE | `/students/1` | Destroy | Delete the existing student whose ID is 1                      |

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
