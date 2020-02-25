---
layout: post
title:      "Rails Project - scribbit"
date:       2020-02-25 18:15:46 +0000
permalink:  rails_project_-_scribbit
---



Scribbit is an expansion on scriptmate where storytellers, content creators, and writers can put "pen to paper" and log all of their story ideas. From using Sinatra to now being able to use Rails, I thought the project would be much easier due to all of the power that comes along with the new tools, but I also realized it gave me more decisions to make. With the new power of Rails, I could add many more features while creating a more robust application mimicking what is out on the app stores of the world today. 

And becuase of this possibility, well, yes I obviously had to go out and explore it. The results were a mixed bag of fear, promise, excitement, defeat, success, low energy levels and much more. I wanted to make sure that if I was going to go off of a previous idea, it needed to be better, that was a must. 

After generating the main skeletal system of my project and sliding in several of it's key organs, it was time for the features. 

To offer you all some background, my models included users, projects, settings, scenes, and characters along with thier various views and controllers. This was all I needed to capture a new project a user wanted to created, but what else? 

Why not add a posts class to allow an admin to create educational posts for the users? Check. 
What about a peer review system to create a many many relationship between users? Sounds, cool, but how can we capture that in code? This was the hard part, but through the help of my good ol' friend, the Internet, I was able to truly well be on my way. 

```
class Review < ApplicationRecord

    belongs_to :project
    # user reviewing project
    belongs_to :reviewee, foreign_key: :reviewee_id, class_name: "User"

    # user wanting project reviewed
    belongs_to :reviewer, foreign_key: :reviewer_id, class_name: "User", optional:true


end
```
This enabled my new review class to link to the user using two foreign keys. 

Meanwhile, this all had to be mapped on the user side as well. 

```
  # can see requested reviews for a user
  has_many :requested_reviews, foreign_key: :reviewee_id, class_name: "Review"
	# can see which users are reviewing the reviewees projects
  has_many :your_reviewers, through: :requested_reviews, source: :reviewer
	# can see which reviews had been accepted by other reviewers 
  has_many :accepted_reviews, foreign_key: :reviewer_id, class_name: "Review"
```

Once these associations had been sent. Essentially what had happened beyond the scenes was a join table between the reviews and the users, alowing the database to trace who the reviewer is and who the reviewee is with respect to a review. 

Overall, there are a lot more features I would like to add to this project to really be able to say it can stand on its own as a complete web application, but for now I am proud of what I had accomplished and looking forward to what is ahead. 
