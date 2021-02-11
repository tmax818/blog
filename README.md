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