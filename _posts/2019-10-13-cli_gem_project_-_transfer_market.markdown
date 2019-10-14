---
layout: post
title:      "CLI Gem Project - Transfer Market"
date:       2019-10-13 15:26:43 -0400
permalink:  cli_gem_project_-_transfer_market
---


Hi Everyone, 

Greetings from a very specific longitude and latitude somewhere on the east coast. 

Today I would like to talk about my first project in the online software engineering course.

Where do I begin? 

Oh, I know. Let us begin from where it all kicked off... The moment our cohort's learning instructor, Jake,  announced to us that our first project was steadiliy approaching. I don't remember exactly how it was presented, but I remember hearing that we needed to come up with our first application that would scrape a URL page and present specifc information based on user inputs. 

At first, I was left nervous thinking, "Me, write an application?!? I've only been doing this[coding] for a little over a month. I hope I'm ready."

Although being a bit nervous, I was confident that the course material presented to us up to this point should have prepared us to build a successful CLI application. 

To start, I watched Avi's video about starting the project very intently and I have to say, I was very grateful this material was made available to us. I worried that I wouldn't be able to have consistent dialogs with Jake to help trouble-shoot any issues that I would run into, specifically on weekends, but Avi's video ensured I was at least able to get started and start generating some output with my code.  

Being a huge soccer fan, I definitely wanted to incorporate my love for the sport into this project so I decided to choose one of my favorite websites, transfermarkt.com, to scrape from. 

In the early stages of my project, I planned for the incorportation of the following steps: 

1. Input a soccer player 
2. Select a soccer player from the list
3. Display information for a soccer player. 

I began laying out the foundation of my project by trying to figure out how to use the user input to target a specifc webpage of where I can start scraping information. 

I found that I can store the query and input it into the url, under input: 
```
https://www.transfermarkt.us/schnellsuche/ergebnis/schnellsuche?query={INPUT}&x=0&y=0
```

Once figuring this out, I was then able to move onto scraping the result page. When I began scraping, I found difficulty because I was iterating through rows for a table where the class value kept alternating between "odd" and "even". I was accustomed to targetting a specific value or tag to get a path and was getting unwanted paths by generalizing the destination, but the below code enabled me to specific with the order of the paths by using '>'. 

```
player_array.css("table.items > tbody > tr").each do |player| 
```

After scraping the right information, I created a new object class to store the information to later be able to print it in the results on the first page. 
Next, I wanted to be able to scrape the results off of all of the pages. Luckily for me, Jake had gone over this in the lesson during the first week of our project. So with the help of his lesson, I was able to see if there was an anchor on the next button and grab the next url to scrape from and wrote the following method: 

```
  def self.next_url
    next_btn = @doc.css("div.row div.box div.responsive-table div.pager li.naechste-seite a")
      if next_btn.attribute("href")
       "https://www.transfermarkt.com" + next_btn.attribute("href").value
      else 
        nil
      end
  end 
```

Since I had already been printing the search results on the first page. I figured I would be able to print all the scraped results at once, but this didn't end too well.. 

My program kept crashing due to the high amount of search results and repeated scraping that was going on behind the scenes. I spoke to Jake about this, and he suggested to use a next button, to only show the additional results based on the user's request. This worked out very well as I was then able to limit the activity on the processing side of my program. 

At this point, I was confident I would finish my program fact, since all I needed to do was now grab the URL associated with the selected player and scrape from there, which was pretty straight forward. This is exactly what I did, and application was swiftly en route to completion so I decided to start exploring formatting options for a better user experience. 

My search lead me to the gem TTY, which allowed a user to use prompts to present a list of choices, highlight them and store the selection. This also allowed for cleaner CLI interactions in the terminal. At this point I was very satisfied with the added quality to UX this provided, so I ditched my old CLI and put all my eggs in the TTY interface. 

This went horribly horribly wrong. I spent many hours restructuring my code based on the demand of TTY and had a sleek and velvety program until I started incorporating my error messages. I had endless loops of text stemming from prompts, and the inclusion of errors was ofsetting my selections. I spent hours in the pry assessing if my stored variables resulted in my desired values, and they did, yet the errors persisted. I felt like I was going backwards, and my effort was leading to dimished returns repeatedly. 

That's when I decided to focus on just having my application run smoothly to include all the features I had worked on, and worring about formatting as the last thing. My application depended on many factors to get to the next page and there were several options on what a user could do, and this complicated my cli file when it came to errors. 

I felt that many times I would impliment a return to notify the user of an error, another part of the program would break. This is when I was thinking about looking into coding test cases, but ultimately decided against it and wrote all my test cases on a piece of paper and went through scenarios to test each one individually. 

After hitting brick walls multiple times over my obsession to insignificant details, I finally was where I wanted. My program worked perfectly and the user was not able to break it based on their inputs. I was thrilled. That's when I started focusing on formatting again, except this time I opted against repimplimenting all the prompts I was using from TTY and decided to use color as a way to give the user a better experience. 

I did some research and came accross pastel, which was actually already built into TTY. This allowed me to make my text various colors and enabled me to change the text style to include bold and underlined text. I made all my error notices red, to catch the user's eye and show them something was wrong. I made my general user communication text yellow, which stood out to the standard white from the input, and added input options magenta as a standout option to show alternative inputs. Also, my player bio info had each attribute in blue to also show a difference between the attribute and the value. 

Overall, I was left very pleased with my project and found this a great opportunity to learn on my own by seeking knowledge and help in a plethora of ways. Whether that be from my peers, learning instructor, the internet or my coworkers, the project enabled me to generate invaluable dialog when it came to coding, which ultimately made me a much better coder than I was two weeks ago. 

Until next time! 
-Umberto

