---
layout: post
title:      "Sinatra Project"
date:       2020-08-02 18:15:24 +0000
permalink:  sinatra_project
---

![](https://www.becomesingers.com/wp-content/uploads/2019/12/Frank-Sinatra.jpg)


The Sinatra Project required a little more brain power to get it working. I am glad that this project is over but there is still a question lingering about this technology in my mind: why was it named after Frank Sinatra. Maybe the creator, Blake Mizerany, was listening to Frank Sinatra that he named it Sinatra. 


Aside from the naming of the technology, I created a CRUD, MVC application that uses Sinatra and ActiveRecord. The application keeps track of gamer's collection of video games using databases created by ActiveRecord and displays results using different routes with Sinatra. The application requires the gamer to login to create or manipulate entries that was created by them. If they do not have an account, the gamer is able to create a new account and start creating entries right away.

For a copy of my application, please go to my [GitHub account](https://github.com/Dice-K39/Sinatra_Project).

## The File Tree
SINATRA_PROJECT                                                                                                                                                                 
|-app                                                                                                                                                                                           
|   |-controllers                                                                                                                                                                           
|   |   |_application_controller.rb                                                                                                                                                   
|   |   |_gamer_controller.rb                                                                                                                                                         
|   |   |_video_game_controller.rb                                                                                                                                                 
|   |-models                                                                                                                                                                                 
|   |   |_gamer.rb                                                                                                                                                                           
|   |   |_video_game.rb                                                                                                                                                                 
|   |-views                                                                                                                                                                                   
|       |-gamers                                                                                                                                                                             
|       |   |_login.erb                                                                                                                                                                       
|       |   |_signup.erb                                                                                                                                                                   
|       |-video_games                                                                                                                                                                   
|       |   |_edit.erb                                                                                                                                                                         
|       |   |_index.erb                                                                                                                                                                     
|       |   |_new.erb                                                                                                                                                                       
|       |   |_show.erb                                                                                                                                                                     
|       |_index.erb                                                                                                                                                                         
|       |_layout.erb                                                                                                                                                                         
|-config                                                                                                                                                                                       
|   |_environment.rb                                                                                                                                                                     
|-db                                                                                                                                                                                             
|   |-migrate                                                                                                                                                                                 
|   |   |_create_gamers.rb                                                                                                                                                             
|   |   |_create_video_games.rb                                                                                                                                                   
|   |   |_add_column_email_to_gamers_table.rb                                                                                                                         
|   |   |_remove_column_producer_from_video_games_table.rb                                                                                                 
|   |   |_rename_column_release_date_to_date_purchased_in_video_games_table.rb                                                               
|   |_schema.rb                                                                                                                                                                           
|-lib                                                                                                                                                                                             
|-public                                                                                                                                                                                       
|   |-images                                                                                                                                                                                 
|   |   |_game_background.jpg                                                                                                                                                     
|   |-javascripts                                                                                                                                                                           
|   |-stylesheets                                                                                                                                                                           
|-.env                                                                                                                                                                                         
|-.gitignore                                                                                                                                                                                 
|-config.ru                                                                                                                                                                                   
|-Gemfile                                                                                                                                                                                     
|-Gemfile.lock                                                                                                                                                                             
|-LICENSE                                                                                                                                                                                 
|-Rakefile                                                                                                                                                                                   
|-README.md                                                                                                                                                                           
|-spec.md                                                                                                                                                                                   


As you can see here, the file tree is large and it can become larger if I decide to add more features to this application such as editing the gamer profile or adding another migration file for a table for consoles.

## The Beginning Process

The process of starting the project was straightforward. 

1. Download the corneal gem using the terminal if not readily available locally.
2. Decide where in your computer to settle the files for the project in and run corneal. Corneal will create the necessary files and folders in the directory of choice.
3. Install necessary gems.

The gems necessary are:

1. sinatra
2. activerecord version 4.2.6 or higher
3. sinatra-activerecord
4. rake
5. require_all
6. sqlite3 version 1.3.6
7. thin
8. shotgun
9. pry
10. bcrypt
11. tux
12. sinatra-flash
13. dotenv
14. rspec
15. capybara
16. rack-test
17. database_cleaner

## Process of the Project

### MVC

#### Models

I started my project by deciding what models I will need. My project is based on video game collections so I have a model for the gamer (i.e. user) and video game. 


This is how my video game model looks like:

```
class VideoGame < ActiveRecord::Base
    belongs_to :gamer

    validates :title, presence: true
    validates :developer, presence: true
    validates :date_purchased, presence: true
    validates :description, presence: true
end
```


And this is how my gamer model looks like:

```
class Gamer < ActiveRecord::Base
    has_secure_password
    has_many :video_games

    validates :username, presence: true, uniqueness: true
    validates :email, presence: true, uniqueness: true
end
```

The association between a gamer and their video game is that the gamer **has many** video game and a video game **belongs to** a gamer. This is a simple has many/belongs to association. In the VideoGame class, the keyword **validates** signifies that the valid data exists for each attribute for the class. Same goes with the Gamer class. The **has_secure_password** is a macro in ActiveRecord that adds useful methods to set and authenticate against a BCrypt password. **BCrypt** is a password hashing gem that salts user entered password from signup which makes hackers work harder to crack the password.

#### Views

Views are where the result is displayed from manipulating data from the database. Most of the things in the Views was html, which was a new learning experience for me. Forms are used to create, update, and delete entries by the gamers that are stored in the database created by ActiveRecord. Database items can also be read with simple html coding. The files I have in my views folder is large so if anyone likes a copy, please go to my [GitHub account](https://github.com/Dice-K39/Sinatra_Project/tree/master/app/views) to retrieve it.

#### Controllers

My controllers are straightforward. I have three: two for the models that I created and one base controller that my model controllers inherit from. 

The ApplicationController does particularly nothing except contain the route to the start page of my application and helper methods that I use throughout my other two controllers.

The GamerController have routes that let gamers create accounts and let them login to their accounts. Many validations are in place in the signup route that checks for the validity of the email and password. The same goes for the login route. This is so that bad data will not persist in the database.

The VideoGameController have routes that create, read, update, and delete video games from the database that the gamer owns. It will not affect any other gamers' video game collection. In creating and updating routes, there are validations in place to check the validity of the entries.

If anyone likes a copy of my controllers, please go to my [GitHub account](https://github.com/Dice-K39/Sinatra_Project/tree/master/app/controllers) to retrieve it.

## Finish Line

Well I finished this project using two weeks and it was a learning experience. Creating a webpage is easy but styling it in a certain way was harder than expected. Hopefully I will be able to pass the assessment coming up with the knowledge that I gained from this module and project.
