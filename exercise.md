# We Do: Real Life MVC

**Student Roles:**

1. Request
- Router
-	Controller
-	Model
-	Index view
-	Show view
-	Runner

#### Requests

`get “/artists”`

`post “/artists”`

`put “/artists/3”`

`delete “/artists/4”`


### Controller Statement List

#### GET (without an id)

- If no ID
  - Then Ask Model for All Artists
- Render View
- Respond to Client

#### GET (with an id)

- Then Ask Model for Artist with given ID
- Render View
- Respond to Client

#### POST

- Then Ask Model to Add New Artist Data
- Render View
- Respond to Client

#### PUT

- Then Ask Model to Edit Artist Data
- Render View
- Respond to Client

#### DELETE

- Then Ask Model to Delete Artist
- Render View
- Respond to Client

### View

```ruby

Index View

<ul>

   <li>

      <a href="/artists/<%= artist.id %>">

		#LIST ARTISTS’ NAMES BELOW:


     <%= ________________________ %>



     <%= ________________________ %>



     <%= ________________________ %>



     <%= ________________________ %>



	<%= ________________________ %>

      </a>

    </li>

</ul>
```

```html
Show View

Add Artist Name Below

<h2> ____________________ </h2>

<ul>

		List Songs’ Titles Below


   <li> <%=_____________________ %> </li>



   <li> <%=_____________________ %> </li>


</ul>
```
