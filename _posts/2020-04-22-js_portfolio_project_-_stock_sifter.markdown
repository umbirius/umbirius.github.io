---
layout: post
title:      "JS Portfolio Project - Stock Sifter"
date:       2020-04-22 16:43:57 +0000
permalink:  js_portfolio_project_-_stock_sifter
---



Alas, here we are once more, another project in the books, but first let's rewind. O, Javascript, what did I do to deserve you? Before, all I knew about app creation was restful routes, but now the game has been changed forever. 

Remember travelling to a foreign country language the words people would speak sounded like some sort of jibberish often depicted in movies? Well, I do, and this is how I felt getting introduced to the world of JS. After "speaking" Ruby for the past 8 months, I had akward feeling of trying to learn how to ride a bike all over again. Although different, I met the occasion with excitement and a slight bit of fear. 

***Fastfoward several weeks...*** And it's project time!!! Time to throw everything I just learned at the wall and see what sticks...then I will casually try to clean up everything on the floor as if it never happened. 

Using what JS has equipped me with, the goal was to create an interactive web application that didn't rely on reloading of the DOM, but rather dynamically changed in response to a user's interaction. Bearing this in mind, I opted for a stock screener application. In my free time I enjoy researching and trading stocks, so I found this a great opportunity to incorporate my interest into my project. 

My thought process in terms of the design was as follows :

*  Seed a bunch of stock data into my backend database that will be used as the foundation of what will be 'screened'. 
*  Next, allow the user access to several modifiable fields that will filter an attribute of a stock. Based on the combination of all of the filter critera, it will return stocks that meet this aggregate filter. 
*  A user then has an option to save this filter and name it based on what that filter represents to them. *(e.g. High Activity Financial stocks under $5)*
*  Once a user saves their filters, they would be able to store this arsenal of curated screeners, and always return to get new prospective plays in the stock market as said market dynamically changes with the passing of time.

**Viola!** And there we have it folks. The way I had defined it before I started sounded so neat, achievable, and quite simple, but the truth of the matter is I was not all too comfortable with creating a fullblown application with JS and Rails. I.e. this meant a lot of failure was to come. So I readied my battle armor (sweatpants), grabbed my sword (laptop) and was off to the arena (my desk) for what was going to be a war. 

At first I set up the database, html page, and JS script to be all linked. Next I started to set up my rails models, controllers, and respective serializers using fastJSON API. 

This enabled me to interact with my Rails models on the JS side of my application for my Stock, User, and Filter models. 

**e.g**
```
class FilterSerializer
  include FastJsonapi::ObjectSerializer
  attributes :id, :name, :market_cap, :sector, :last_price, :fiftytwo_high, 
    :fiftytwo_low, :vol, :avg_vol, :rel_vol, :insider_own, :inst_own, :user_id
  belongs_to :user
end
```

Next came the fun of JS with the various fetch requests to get the inital data to populate my front end and to post new model creations on the backend. And in between being able to use those objects on the front end side too. 

To stay organized I would have three JS classes to mirror the backend models and navigate through both with consistency. 

My Filter and User classes would be created with stringified JSON data, therefore only had one argument. 

```
class User {
  constructor(user) {
    this.name = user.name
    this.id = user.id
  }
}
```

```
class Filter {
  constructor(filter) {
    this.id = filter.id;
    this.name = filter.name;
    this.price = filter.last_price;
    this.volume = filter.vol;
    this.avgVolume = filter.avg_vol;
    this.relVolume = filter.rel_vol;
    this.sector = filter.sector;
    this.marketCap = filter.market_cap;
    this.fiftytwoWeekHigh = filter.fiftytwo_high;
    this.fiftytwoWeekLow = filter.fiftytwo_low;
    this.insiderOwn = filter.insider_own;
    this.instOwn = filter.inst_own;
    this.userId = filter.user_id
  }
}
```

On top of this I kneaded static methods and instance methods into each class to create a more robust application.

Examples of these are below 

* resetFilter helped reset the filter options when a user clicked on a reset button. 

```
  static resetFilter() {
    let searchIds = ['price', 'volume', 'avg-volume', 'rel-volume', 'sector',
      'market-cap', '52-week-high', '52-week-low', 'insider-own', 'inst-own']
    for (let id of searchIds) {
      document.getElementById(id).value = "any"
    }
  }
```

* loadFilters is called on a user instance to load all of that user's filters  
```
  loadFilters() {
    fetch('http://localhost:3000/filters')
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        let filterSelection = document.getElementById("load-filter")
        let userFilters = data.data.filter(filter => filter.attributes.user_id === this.id)
        for (let filter of userFilters) {
          let option = document.createElement("option")
          option.value = filter.attributes.name
          option.text = filter.attributes.name
          option.setAttribute("id", filter.attributes.id)
          filterSelection.appendChild(option)

        }
        filterSelection.value = "none"
      })
  }
```

Ultimately, through trial, error, and an incredible amount of refactoring. I started to get the feel of how to scope with JS, which was my biggest difficulty in the beginning, and towards the end of my coding my project, I was able to add features and functionality more smoothly.

Looking at my project, I truly appreciate the value Javascript has provided me in terms of possibilities in functionality and user experience. The time in the arena paid off and I am now ready for bigger battles thanks to the help of my friend, Javascript. 





