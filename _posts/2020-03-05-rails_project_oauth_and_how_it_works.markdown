---
layout: post
title:      "Rails Project: oAuth and How it Works"
date:       2020-03-05 13:53:03 -0500
permalink:  rails_project_oauth_and_how_it_works
---


So we've all used oAuth for our rails project, not really out of desire, but more so out of necessity being a project require emnt and all that is. Don't get me wrong, it's an amazing gem that adds an added layer of authentication in one's app, but when considering what it does, it just seemed all too complicated to someone with limited experience in authentication. 

Don't worry, it's really not that complicated. Imagine placing an order for pick up, but you can't quite pick it up yourself. What do you do? Some stores allow you to add an alternate person for pickup. To some extent, that's how oAuth works. 

A user will attempt to log into an application, but without credentials built directly in that application. This would be like attempting to pick up an order, but you're not the person who ordered the item. 

Rather what the user will do is log in using credentials on another application (Facebook, Google, Github, etc..). The other application is like an alternate user picking up the order. 

How does that outside application know of the rails application, vice versa? They will be linked to eachother by way of a secret and client ID. A project must be registered on the developer side of an application. Once the project is registered, the secret and client ID can be added to the Rails app as a way to pass them to the client (Facebook, Google, Github, etc..). This would be the alternate user for pickup and the secret/clientID is the order number and form of identification and the primary person who placed the order adding a alternate user to the order log. 

When I am now logging in to let's say Facebook with my Facebook crendentials, The app will send the client ID to Facebook. Facebook will receive this ID and if they match, next, facebook will check the project secret will grant me permission to log into the app and redirect me to the redirect page I set on my project in the Developer site. This would be the same as me handing the clerk and order number and my ID to confirm that I can infact pick up the object. 

The end result is the same, I have been able to pick up the order without ever placing an order, or in the Rails project case, I have been granted permission to the app without ever making an account on the app itself. 



