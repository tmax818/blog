# blog

These are my notes for the [Rails Guides](https://guides.rubyonrails.org/index.html)

# Start Here

## [1 Guide Assumptions](https://guides.rubyonrails.org/getting_started.html#guide-assumptions)

- Designed for Rails beginners
- "Rails is a web application framework running on the Ruby programming language."
- You should know Ruby:
  - [Official Ruby Programming Language website]
  - [List of Free Programming Books]

## [2 What is Rails?](https://guides.rubyonrails.org/getting_started.html#what-is-rails-questionmark)

>Rails is a web application development framework written in the Ruby programming language. It is designed to make programming web applications easier by making assumptions about what every developer needs to get started. It allows you to write less code while accomplishing more than many other languages and frameworks. Experienced Rails developers also report that it makes web application development more fun.


- Two Guiding Principles:
1. DRY 
>"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."
- DRY code is:
  - maintainable
  - extensible
  - less buggy
2. Convention Over Configuration
>"Rails has opinions about the best way to do many things in a web application, and defaults to this set of conventions, rather than require that you specify minutiae through endless configuration files."

## [3 Creating a New Rails Project](https://guides.rubyonrails.org/getting_started.html#creating-a-new-rails-project)

- follow step by step

### [3.1 Installing Rails](https://guides.rubyonrails.org/getting_started.html#creating-a-new-rails-project-installing-rails)

- Prerequisites:
  - [Ruby]
  - [Sqlite3]
  - [Node.js]
  - [Yarn]

### [3.2 Creating the Blog Application](https://guides.rubyonrails.org/getting_started.html#creating-the-blog-application)

- [generators]
- since I already have this file as a repo I will run this command:

```bash
$ rails new .
```

|File/Folder|Purpose|
|---|---|
|[`app/`](app/notes.md)|Contains the controllers, models, views, helpers, mailers, channels, jobs, and assets for your application. You'll focus on this folder for the remainder of this guide.|
|[`bin/`](bin/notes.md)|Contains the rails script that starts your app and can contain other scripts you use to set up, update, deploy, or run your application.|
|[`config/`](config/notes.md)|Contains configuration for your application's routes, database, and more. This is covered in more detail in [Configuring Rails Applications].|
|[`config.ru/`](config.ru)|Rack configuration for Rack-based servers used to start the application. For more information about Rack, see the [Rack website].|
|[`README.md`](.)|This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on.|


## [4 Hello, Rails!](https://guides.rubyonrails.org/getting_started.html#hello-rails-bang)

### [4.1 Starting up the Web Server](https://guides.rubyonrails.org/getting_started.html#starting-up-the-web-server)

- run:

```bash
$ rails s
```

### [4.2 Say "Hello", Rails](https://guides.rubyonrails.org/getting_started.html#say-hello-rails)

- You need:
  - [route](config/routes.rb) 
    -  maps a request to a controller action.
    -  rules written in a Ruby DSL
  - [controller and an action](app/controllers/application_controller.rb) 
    - handles the request and prepares the data.
    - Ruby classes and public methods are actions
  - [view](app/views/notes.md) 
    - displays data in desired format. 
    - templates written in Ruby and HTML

- [create the route](config/routes.rb)
- Generate the controller:

```bash
$ rails generate controller Articles index --skip-routes
```

- [Most important](app/controllers/articles_controller.rb)

>The index action is empty. When an action does not explicitly render a view (or otherwise trigger an HTTP response), Rails will automatically render a view that matches the name of the controller and action. Convention Over Configuration! Views are located in the [app/views](app/views/notes.md) directory. So the index action will render [app/views/articles/index.html.erb](app/views/articles/index.html.erb) by default.

- [change the content](app/views/articles/index.html.erb)
- [visit](http://localhost:3000/articles)

### [4.3 Setting the Application Home Page](https://guides.rubyonrails.org/getting_started.html#setting-the-application-home-page)

- [add root route](config/routes.rb)

- learn more about [routing]

## [5 MVC and You](https://guides.rubyonrails.org/getting_started.html#mvc-and-you)

- MVC - "a design pattern that divides the responsibilities of an application to make it easier to reason about."


### [5.1 Generating a Model](https://guides.rubyonrails.org/getting_started.html#mvc-and-you-generating-a-model)

- model - "a Ruby class that is used to represent data."

```bash
R rails g[enerate[] model Article title:string body:text
```

>Model names are singular, because an instantiated model represents a single data record. To help remember this convention, think of how you would call the model's constructor: we want to write `Article.new(...)`, not `Articles.new(...)`.

- Two files we focus on
  - [migration](db/migrate/20210211222316_create_articles.rb)
  - [model](app/models/article.rb)


### [5.2 Database Migrations](https://guides.rubyonrails.org/getting_started.html#database-migrations)

- migrations:

>*Migrations* are used to alter the structure of an application's database. In Rails applications, migrations are written in Ruby so that they can be database-agnostic.

- check out [migration](db/migrate/20210211222316_create_articles.rb)

- run the migration with:

```bash
$ rails db:migrate
```
- we get this cool shit!
```
==  CreateArticles: migrating ===================================
-- create_table(:articles)
   -> 0.0018s
==  CreateArticles: migrated (0.0018s) ==========================
```

You learn more about [Active Record Migrations]. "Now we can interact with the table using our model."


### [5.3 Using a Model to Interact with the Database](https://guides.rubyonrails.org/getting_started.html#using-a-model-to-interact-with-the-database)

- use the rails console to play with our models:

```bash
[views (mvc-and-you)]$ rails c
Running via Spring preloader in process 85912
Loading development environment (Rails 6.1.2.1)
>> article = Article.new(title: "Hello Rails", body: "I am on Rails!")
   (0.4ms)  SELECT sqlite_version(*)
=> #<Article id: nil, title: "Hello Rails", body: "I am on Rails!", created_at: nil, updated_at: nil>
>> article.save
  TRANSACTION (0.1ms)  begin transaction
  Article Create (3.0ms)  INSERT INTO "articles" ("title", "body", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "Hello Rails"], ["body", "I am on Rails!"], ["created_at", "2021-02-11 22:36:52.545193"], ["updated_at", "2021-02-11 22:36:52.545193"]]
  TRANSACTION (18.3ms)  commit transaction
=> true
>> 
```

You learn more [Active Record Basics] and [Active Record Query Interface]

### [5.4 Showing a List of Articles](https://guides.rubyonrails.org/getting_started.html#showing-a-list-of-articles)

- [Change the index action](app/controllers/articles_controller.rb) by adding `@articles = Article.all`
- [use the instance variable in the view](app/views/articles/index.html.erb)

```ruby
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= article.title %>
    </li>
  <% end %>
</ul>
```

- `<% %>` = "evaluate the enclosed Ruby code."
- `<%= %>` = "evaluate the enclosed Ruby code, and output the value it returns." 


- seven things

1. The browser makes a request: GET http://localhost:3000.
1. Our Rails application receives this request.
1. The Rails router maps the root route to the index action of ArticlesController.
1. The index action uses the Article model to fetch all articles in the database.
1. Rails automatically renders the app/views/articles/index.html.erb view.
1. The ERB code in the view is evaluated to output HTML.
1. The server sends a response containing the HTML back to the browser.


## [6 CRUDit Where CRUDit Is Due](https://guides.rubyonrails.org/getting_started.html#crudit-where-crudit-is-due)

- Almost all web apps involve CRUD!!
- 6 is long, Bro!

### [6.1 Showing a Single Article](https://guides.rubyonrails.org/getting_started.html#showing-a-single-article)

- [add a new route](config/routes.rb)
- [add the show action](app/controllers/articles_controller.rb)

```ruby
  def show
    @article = Article.find(params[:id])
  end
  ```
- [add the view](app/views/articles/show.html.erb)
- [test](http://localhost:3000/articles/1)
- [add links to index](app/views/articles/index.html.erb)
- [test](http://localhost:3000/articles/)

### [6.2 Resourceful Routing](https://guides.rubyonrails.org/getting_started.html#resourceful-routing)

>Whenever we have a combination of routes, controller actions, and views that work together to perform CRUD operations on an entity, we call that entity a **resource**. For example, in our application, we would say an article is a resource. Rails provides a routes *method* named [resources] that maps all of the conventional routes for a collection of resources, such as articles. 

- [replace the get routes](config/routes.rb)

```bash
[blog (CRUDit)]$ rails routes
      Prefix Verb   URI Pattern                       Controller#Action
        root GET    /                                 articles#index
    articles GET    /articles(.:format)               articles#index
             POST   /articles(.:format)               articles#create
 new_article GET    /articles/new(.:format)           articles#new
edit_article GET    /articles/:id/edit(.:format)      articles#edit
     article GET    /articles/:id(.:format)           articles#show
             PATCH  /articles/:id(.:format)           articles#update
             PUT    /articles/:id(.:format)           articles#update
             DELETE /articles/:id(.:format)           articles#destroy
```

>The [resources] method also sets up URL and path helper methods that we can use to keep our code from depending on a specific route configuration. The values in the "Prefix" column above plus a suffix of `_url` or `_path` form the names of these helpers. For example, the `article_path` helper returns `"/articles/#{article.id}"` when given an article. We can use it to tidy up our links in [index](app/views/articles/index.html.erb):

change:

```ruby
"/articles/<%= article.id %>"
to 
"<%= article_path(article) %>"
```

>However, we will take this one step further by using the [link_to] helper. The `link_to` helper renders a link with its **first argument** as the link's text and its **second argument** as the link's destination. If we pass a model object as the **second argument**, `link_to` will call the appropriate path helper to convert the object to a path. For example, if we pass an article, `link_to` will call article_path. So [index](app/views/articles/index.html.erb) becomes:


```ruby
link_to(name = nil, options = nil, html_options = nil, &block)
```

```ruby
# <a href="<%= article_path(article) %>">
# <%= article.title %> becomes:
 <%= link_to article.title, article %>
 ```
Nice!

You learn more: [routing]


### [6.3 Creating a New Article](https://guides.rubyonrails.org/getting_started.html#creating-a-new-article)

>Typically, in web applications, creating a new resource is a multi-step process. 
- First, the user requests a form to fill out. Then, 
- Second, the user submits the form. 
- If there are no errors, then the resource is created and some kind of confirmation is displayed. 
- Else, the form is redisplayed with error messages, and the process is repeated.
In a Rails application, these steps are conventionally handled by a controller's `new` and `create` actions.

- [add `new` and `create`](app/controllers/articles_controller.rb)

```ruby
  def new
    @article = Article.new
  end
```


>The `new` action instantiates a new article, but does not save it. This article will be used in the view when building the form. By default, the new action will render [new view](app/views/articles/new.html.erb)

```ruby
  def create
    @article = Article.new(title: "...", body: "...")

    if @article.save
      redirect_to @article
    else
      render :new
    end
  end
```

>The `create` action instantiates a new article with values for the title and body, and attempts to save it. If the article is saved successfully, the action redirects the browser to the article's page at "http://localhost:3000/articles/#{@article.id}". Else, the action re-displays the form by rendering [new](app/views/articles/new.html.erb). The title and body here are dummy values. After we create the form, we will come back and change these.

>[redirect_to] will cause the browser to make a new request, whereas [render] renders the specified view for the current request. **It is important to use [redirect_to] after mutating the database or application state.** Otherwise, if the user refreshes the page, the browser will make the same request, and the mutation will be repeated.

[redirect_to] - causes the browser to make a new request
[render] - renders the view 

#### [6.3.1 Using a Form Builder](https://guides.rubyonrails.org/getting_started.html#using-a-form-builder)

- [create the new form using *form builder*](app/views/articles/new.html.erb)
- [form_with]
- [label]
- [text_field]

You learn more: [Action View Form Helpers]

#### [6.3.2 Using Strong Parameters](https://guides.rubyonrails.org/getting_started.html#using-strong-parameters)

>Submitted form data is put into the params Hash, alongside captured route parameters.

You learn more: [Action Controller Overview § Strong Parameters]

#### [6.3.3 Validations and Displaying Error Messages](https://guides.rubyonrails.org/getting_started.html#validations-and-displaying-error-messages)

- [add validations](app/models/article.rb)
- [modify](app/views/articles/new.html.erb)

>The [full_messages_for] method returns an array of user-friendly error messages for a specified attribute. If there are no errors for that attribute, the array will be empty.

You learn more: [Active Record Validations](https://guides.rubyonrails.org/active_record_validations.html)

#### [6.3.4 Finishing Up](https://guides.rubyonrails.org/getting_started.html#creating-a-new-article-finishing-up)

- [link from the index page](app/views/articles/index.html.erb)

### [6.4 **Updating(U)** an Article](https://guides.rubyonrails.org/getting_started.html#updating-an-article)

- Updating
  1. user requests a form to edit the data. Then, 
  2. the user submits the form. 
  3. If there are no errors, then the resource is updated. 
  4. Else, the form is redisplayed with error messages, and the process is repeated.

- [add `edit` and `update` actions](app/controllers/articles_controller.rb)

```ruby
  def edit
    @article = Article.find(params[:id])
  end
```
- `edit` fetches resource from database

```ruby
  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit
    end
  end
```

- `update` action (re-)fetches the article from the database, and attempts to update it with the submitted form data filtered by article_params. If no validations fail and the update is successful, the action redirects the browser to the article's page. Else, the action re-displays the form, with error messages, by rendering app/views/articles/edit.html.erb.

#### [6.4.1 Using Partials to Share View Code](https://guides.rubyonrails.org/getting_started.html#using-partials-to-share-view-code)

- The new and update forms are the same. Be DRY, use a partial!
- create a partial with:

```bash
$ touch app/views/articles/_form.html.erb
```
- [paste the form in the partial](app/views/articles/_form.html.erb)
- But, checkout the difference between the two forms

```ruby
<%= form_with model: article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <% article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <% article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
- Old form:

```ruby
<h1>New Article</h1>

<%= form_with model: @article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
        <% @article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
        <% @article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

- Update both with [render]:
  - [new](app/views/articles/new.html.erb)
  - [edit](app/views/articles/edit.html.erb)
 
You learn more [ Layouts and Rendering in Rails § Using Partials](https://guides.rubyonrails.org/layouts_and_rendering.html#using-partials)


#### [6.4.2 Finishing Up](https://guides.rubyonrails.org/getting_started.html#updating-an-article-finishing-up)

- [link to `edit` from `show`](app/views/articles/show.html.erb)

### [6.5 Deleting an Article](https://guides.rubyonrails.org/getting_started.html#deleting-an-article)

>Deleting a resource is a simpler process than creating or updating. It only requires a route and a controller action.

- [route](config/routes.rb) is already there with the [resources] method.
- [add the controller action0](app/controllers/articles_controller.rb)

```ruby
  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to root_path
  end
```
>The destroy action fetches the article from the database, and calls [destroy] on it. Then, it redirects the browser to the root path.

- [add it to the show](app/views/articles/show.html.erb)

```ruby
link_to "Destroy", article_path(@article), method: :delete, data: { confirm: "Are you sure?" }
```
In the above code, we're passing a few additional options to [link_to]. The `method: :delete` option causes the link to make a `DELETE` request instead of a `GET` request. The `data: { confirm: "Are you sure?" }` option causes a confirmation dialog to appear when the link is clicked. If the user cancels the dialog, the request is aborted. Both of these options are powered by a feature of Rails called **Unobtrusive JavaScript (UJS)**. The JavaScript file that implements these behaviors is included by default in fresh Rails applications.

You learn more [Working With JavaScript in Rails]


## [7 Adding a Second Model](https://guides.rubyonrails.org/getting_started.html#adding-a-second-model)

>It's time to add a second model to the application. The second model will handle comments on articles.

### [7.1  Generating a Model](https://guides.rubyonrails.org/getting_started.html#adding-a-second-model-generating-a-model)

```bash
$ bin/rails generate model Comment commenter:string body:text article:references

```

This creates 4 files:
1. [migration](db/migrate/20210213060524_create_comments.rb)
2. [model](app/models/comment.rb)
3. [test](test/models/comment_test.rb)
4. [test fixtures](test/fixtures/comments.yml)

>You'll need to edit [the article model](app/models/article.rb) to add the other side of the association

You learn more [Active Record Associations]

### [7.3 Adding a Route for Comments](https://guides.rubyonrails.org/getting_started.html#adding-a-route-for-comments)

- [add a route](config/routes.rb)

You learn more [routing]

### [7.4 Generating a Controller](https://guides.rubyonrails.org/getting_started.html#generating-a-controller)

```bash
$ rails g[enerate] controller Comments
```

- created 4 files:
  - [controller](app/controllers/comments_controller.rb)
  - [view](app/views/comments)
  - [helper](app/helpers/comments_helper.rb)
  - [tests](test/controllers/comments_controller_test.rb)

- [update show](app/views/articles/show.html.erb)

- [make the `create` action](app/controllers/comments_controller.rb):

- [update show](app/views/articles/show.html.erb)

## [8 Refactoring](https://guides.rubyonrails.org/getting_started.html#refactoring)

- [clean up the articles#show](app/views/articles/show.html.erb)








[Official Ruby Programming Language website]: https://www.ruby-lang.org/en/documentation/
[List of Free Programming Books]: https://github.com/EbookFoundation/free-programming-books/blob/master/books/free-programming-books.md#ruby
[Ruby]: https://www.ruby-lang.org/en/documentation/installation/
[Sqlite3]: https://www.sqlite.org/
[Node.js]: https://nodejs.org/en/download/
[Yarn]: https://classic.yarnpkg.com/en/docs/install
[Configuring Rails Applications]: https://guides.rubyonrails.org/configuring.html
[Rack website]: https://rack.github.io/
[routing]: https://guides.rubyonrails.org/routing.html
[Active Record Migrations]: https://guides.rubyonrails.org/active_record_migrations.html
[Active Record Basics]: https://guides.rubyonrails.org/active_record_basics.html
[Active Record Query Interface]: https://guides.rubyonrails.org/active_record_querying.html
[resources]: https://api.rubyonrails.org/v6.1.2.1/classes/ActionDispatch/Routing/Mapper/Resources.html#method-i-resources
[link_to]: https://api.rubyonrails.org/v6.1.2.1/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to
[routing]: https://guides.rubyonrails.org/routing.html
[redirect_to]: https://api.rubyonrails.org/v6.1.2.1/classes/ActionController/Redirecting.html#method-i-redirect_to
[render]: https://api.rubyonrails.org/v6.1.2.1/classes/AbstractController/Rendering.html#method-i-render
[form_with]: https://api.rubyonrails.org/v6.1.2.1/classes/ActionView/Helpers/FormHelper.html#method-i-form_with
[label]: https://api.rubyonrails.org/v6.1.2.1/classes/ActionView/Helpers/FormBuilder.html#method-i-label
[text_field]: https://api.rubyonrails.org/v6.1.2.1/classes/ActionView/Helpers/FormBuilder.html#method-i-text_field
[Action View Form Helpers]: https://guides.rubyonrails.org/form_helpers.html
[Action Controller Overview § Strong Parameters]: https://guides.rubyonrails.org/action_controller_overview.html#strong-parameters
[full_messages_for]: https://api.rubyonrails.org/v6.1.2.1/classes/ActiveModel/Errors.html#method-i-full_messages_for
[destroy]: https://api.rubyonrails.org/v6.1.2.1/classes/ActiveRecord/Persistence.html#method-i-destroy
[Working With JavaScript in Rails]: https://guides.rubyonrails.org/working_with_javascript_in_rails.html
[Active Record Associations]: https://guides.rubyonrails.org/association_basics.html