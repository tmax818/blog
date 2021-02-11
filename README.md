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
|`app/`|Contains the controllers, models, views, helpers, mailers, channels, jobs, and assets for your application. You'll focus on this folder for the remainder of this guide.|
|`README.md`|This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on.|





[Official Ruby Programming Language website]: https://www.ruby-lang.org/en/documentation/
[List of Free Programming Books]: https://github.com/EbookFoundation/free-programming-books/blob/master/books/free-programming-books.md#ruby
[Ruby]: https://www.ruby-lang.org/en/documentation/installation/
[Sqlite3]: https://www.sqlite.org/
[Node.js]: https://nodejs.org/en/download/
[Yarn]: https://classic.yarnpkg.com/en/docs/install



