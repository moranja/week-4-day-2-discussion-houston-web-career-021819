# Forms, CRUD and Active Record Associations

Take 30 minutes and discuss the following with your table group. Try whiteboarding out different solutions and ideas!

1. Map the CRUD actions (create, read, update, delete) to their matching Sinatra routes and HTTP verbs. For example: In a blog app, displaying the content of one particular blog post corresponds to the "Read" CRUD action and the *show* RESTful route. The matching route would be an HTTP Get request to '/posts/:id' where the id is that particular post's id i.e. '/posts/6' .

      CRUD          Sinatra routes                                  HTTP verb
      Create       '/pets/new' & '/pets'(redirected)                GET, then POST
      Read         '/pets' & '/pets/:id'                            GET
      Update       '/pets/:id/edit' & '/pets/:id'(redirected)       GET, then PATCH (masked in POST)
      Delete       '/pets/:id/edit' & '/pets'                       GET, then DELETE (masked in POST)

2. Build an HTML form to create a new blog post. Then, build a form to edit a post. What are the differences between the two? What routes do they send requests to? What type of requests should each form make?

```html
<h1>New pet</h1>
<form method="POST" action="/pets">
    <input type="text" name="pet[name]" />
    <input type="text" name="pet[age]" />
    <input type="text" name="pet[breed]" />

    <input type="submit" />
</form>

<h1>Update pet</h1>
<form method="POST" action="/pets/<%= @pet.id %>">
    <input type="hidden" name="_method" value="PATCH" />

    <input type="text" name="pet[name]" value="<%= @pet.name %>"/>
    <input type="text" name="pet[age]" value="<%= @pet.age %>"/>
    <input type="text" name="pet[breed]" value="<%= @pet.breed %>"/>

    <input type="submit" />
</form>
```

3. Revisit your CRUD action-to-route map. What view files, if any, does each action/route correspond to?
    -CREATE - new.erb, READ - index.erb (for all), show.erb (for one), UPDATE - edit.erb, DELETE - usually found on edit.erb
4. Write out the Active Record code to preform CRUD actions on a Post model.
```ruby

class AppliationController < Sinatra::Base

    #CREATE
    get '/posts/new' do
      erb :new
    end

    post '/posts' do
      post = Post.create(params[:post])
      redirect '/posts/#{post.id}'
    end

    #READ
    get '/posts/:id' do
      @post = Post.find(params[:id])
      erb :show
    end

    get '/posts' do
      @posts = Post.all
      erb :show
    end

    #UPDATE
    get '/posts/:id/edit' do
      @post = Post.find(params[:id])
      erb :edit
    end

    patch '/posts/:id' do
      post = Post.find(params[:id])
      post.update(params[:post])
      redirect '/posts/#{post.id}'
    end

    #DELETE
    delete '/posts/:id' do
      post = Post.find(params[:id])
      post.delete
      redirect '/posts'
    end
end

#Why you should use "namespace"
#pet.update()
#params = {_method => "PATCH", pet = {name => 'fido', age => '4', breed => 'corgi'}}

```
5. Let's think about the domain model for a To-Do list application. Let's say you have a List model and an Item model.
  * What is the relationship between a list and an item?
    -A list can have many items, and item has one list, so one-to-many
  * A user needs to be able to visit your app, create a new list and then add items to that list. What route would bring the user to the the page to make a new list? What route would take them to the page to make a new item?
    -'/lists/new', '/items/new'
  * How and where would you write the code that associates a new item to its list?
    -ItemController.rb,

    POST "/whatever" do
      item = Item.create(params[item])
      item.list = params[list_id]
    end
