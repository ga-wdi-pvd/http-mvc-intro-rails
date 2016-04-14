# We Do – In person MVC role plays

**Student Roles:**

1.	request
2.	controller
3.	runner
4.	model
5.	index view
6.	show view

**Requests**

get “/artists”

post “/artists”

put “/artists/:3”

delete “/artists/:4”


**Controller Statement List**

- If receive a GET request
  - If no ID
    - Then Ask Model for All Artists
  - Render View
  - Respond to Client

- Elsif  has ID
  - Then Ask Model for Artist with given ID
  - Render View
  - Respond to Client

- Elsif  receive a POST request
  - Then Ask Model to Add New Artist Data
  - Render View
  - Respond to Client

- Elsif  receive a PUT request with an ID
  - Then Ask Model to Edit Artist Data
  - Render View
  - Respond to Client

- Elsif receive a Delete request with an ID
  - Then Ask Model to Delete Artist
  - Render View
  - Respond to Client

**Views**

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
