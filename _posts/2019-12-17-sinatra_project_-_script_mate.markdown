---
layout: post
title:      "Sinatra Project - Script Mate"
date:       2019-12-17 16:32:52 -0500
permalink:  sinatra_project_-_script_mate
---

As a fan of cartoons and television in general, I always wanted to create my own stories and content. My biggest struggle has always been organizing my ideas, but I never chose to do anything about it...***Queue the music*** Until now. It was that time in the bootcamp curriculum, where many other cohort students along with myself were faced the challenge of developing our very first Sinatra Web Application from scratch. ***Queue the music once more***, this time let's make sure its dramatic. The world was my oyster as the topic of my project was entirely up to me to decide as long as I incorporated all the CRUD and MVC requirements. I knew I wanted to create something with a real world application, so obviously my first thought was, "Pokemon team creator app!". Everyone knows that Pokemon teams are a highly important part of day to day life, but then I thought of something just a bit more useful. Remember that story of me struggling to organize my content? I'm sure I am not alone with my ability to be organized and thought an actually helpful project would be a tool to help organize the creation of stories and their content. Hence Script Mate was born. 

The first thing was getting all of the configurations ready (config.ru, environment, gemfile, bundler, etc..). Once this was done, I started by creating users and projects. With a user having many projects and and a project belonging to a user. The next thing was make sure when started up my config.ru file that I was able to connect to a server. The server connected and my initial routes displayed my early views. Success! I thought, but there was a lot more to be done. I needed to make sure that certain projects were only displayed when the user the project belonged to was logged in. This was done by linking a project to the activeuser when it was created. 

```
    def project_params
        { name: params[:name], bio: params[:bio], artform: params[:artform], genre: params[:genre], user: current_user}
    end 
```

Next up, MORE BRANCHES! If I'm making a project I would like some characters, settings, and maybe scenes, right? Right. So I threw those in as well. At this point, going through my checklist. Yes I had my basic MVC set up going, but what about my CRUD? Create, Read, Update, and Delete. C and R, Check!  I left my U and D on the back burner until I laid out all the readable data I deemed necessary. Once that was ready, I was ready. I made my update and delete routes with their complementary views and viola, there it was. My CRUD, MVC (I know a lot of acronyms) was ready for the world, and by world I mean github, and by github, really just my project reviewer, but I was satisfied nontheless. My first interactive application with the ability to create, read, update, and delete objects. I also added the edit and delete feature for specific projects on the index page of all projects to enable a user to have an overview of their current projects as they made changes. 

```
<h3><%= @user.username %>'s Projects</h3>
<div class="table-responsive">          
<table class="table">
  <thead>
    <tr>
      <th>Project Name</th>
      <th>Art Form</th>
      <th>Genre</th>
      <th>Description</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>

    <% @projects.each do |project| %>
        <tr>
            <td><a href="/projects/<%=project.id%>"><%= project.name%></a></td>
            <td><%= project.artform%></td>
            <td><%= project.genre%></td>
            <td><%= project.bio%></td>
            <td><a href="/projects/<%= project.id %>/edit" class=" btn btn-default btn-xs">Edit</a></td>
            <td>
                <form method='POST' action="/projects/<%= project.id %>/delete">
                <input type="hidden" name="_method" value="delete">
                <input type="submit" class="btn btn-default btn-xs" value="Delete">
                </form>
            </td>
            
        </tr>
    <% end %> 
```

Although I was technically done with the project requirements, I wanted to make the application experience as realistic as possible and added a user profile page, a home page with a daily feed, and an about page. Sprinkle a little CSS on top (although the CSS portion of this project really gave me more than I had bargained for) and there it is: Script Mate. 



