---
layout: post
title:  "How I Became the Problem in My Grandpa's Fantasy Golf League"
date: 26-09-14
description: Using data cleaning, feature engineering, and a little golf knowledge to take on my grandpa's fantasy golf league. 
image: "/assets/img/pgatrophy.jpeg"

---
<p class="intro"><span class="dropcap">I</span>f you know me, you know I can't say no to a competition. So when my grandpa asked if I wanted to join his fantasy golf league, there was only one right answer. Not only was I in, but I was in it to win it. With that being said, here's my (belated) guide to beating your grandpa and all his friends at fantasy golf (with a little help from data.) </p>

### Background & Life update 

So now that I got you with a hook, let's dive into how I even got into this situation. If I had loyal readers, they would probably be wondering where I've been for the last year. The answer is pretty exciting: I started a Master's in Statistics and got married! It's been a fun year, but unfortunately, all the time I used to spend on passion projects turned into time spent working on my thesis and deciding on table runners.

That being said, I'm excited to have a little extra free time. Before I jump into new projects, I wanted to document a few of the ones I was able to squeeze into my very busy schedule.

Okay, now into the project. Last winter, my grandpa asked my fiancé (now husband) and me if we wanted to join his fantasy golf league. This league is full of his friends, so by joining, we would be the youngest team in the group by at least 25 years. We knew that if we were going to do this, we had to prove that we weren't just a charity case.

The only problem? We got a late invite. While the other teams had the entire PGA offseason to research and plan, we had three days. And these three days happened to be four months before our wedding and the start of a new semester. (Don't ask me how we did all of this at once.)

So we had to be smart, not only about our time, but about what information was actually worth looking at.

#### League Setup
The fantasy league we played in is a little different from a standard football fantasy league. Instead of doing a draft, teams are given a fake budget that they use to "buy" players. Each team needs 10 players, and you can't go over the budget. Multiple teams can have the same players, but your team stays the same for the entire season.

The scoring system is based on how much prize money your players make each week. So basically, we had to do our research, choose our 10 golfers, and then sit back for the rest of the year and hope we knew what we were doing.

### Data
The league is run through [Buzz Fantasty Golf](https://buzzfantasygolf.com/), so we started with the resources they provided about golfer salaries and then combined that with performance data from the PGA website from the previous season.

My husband is an Excel wizard, so he handled a lot of the initial data cleaning and made sure the golfer names matched across the different sources. Once we had everything in one place, it was time for me to figure out what we actually cared about.

### Feature Engineering
A lot of times when I have a project like this, my mind immediately turns to whatever machine learning or regression model I've learned most recently. When I started brainstorming ideas, though, I realized that I needed to simplify my thinking.Sometimes the simplest answer really is the best one.

In this case, we didn't want a model to spit out a black-box ranking and tell us who to pick. We wanted to quickly evaluate skill, consistency, and cost so we could combine the numbers with our own golf knowledge and make the final decisions ourselves.

This is where feature engineering came in. Instead of just looking at the raw statistics available to us, we created a few new variables that we thought would better capture what we actually cared about.

#### Events Played
This one is maybe a little obvious, but it was an important first step. Because our points were based on prize money, we needed players who weren't just playing a lot of tournaments, but were playing in tournaments where there was actually a lot of money to be made. The biggest purses were found in the majors and signature events, so we created a variable for how many of these events each golfer was invited to play in during the previous season. If a golfer had played in fewer than five of these events, we didn't even look at them.

#### Cuts Made & Top 25 Made
Similarly, you make more money if you make it farther in a tournament. So we created variables for how many times each golfer made the cut and how many times they finished in the top 25.

These gave us a basic picture of consistency and performance. But raw counts don't tell the whole story.A golfer who played 30 tournaments and made 15 cuts isn't necessarily more consistent than someone who played 20 tournaments and made 14 cuts. So we started turning these counts into ratios.

#### Cuts Rate
This is where we started getting to the information we actually cared about. We calculated Cuts / Events to measure how consistently a golfer made the cut when given the opportunity.
For this feature, we wanted a higher ratio. If a player plays in a lot of events but regularly misses the cut, we'd rather have someone who plays fewer events but consistently makes money when they do. In other words, instead of simply asking, "How often does this golfer play?" we were asking, "How efficiently does this golfer turn opportunities into points?"

#### Top 25 Rate
We took the same idea one step further with Top 25 / Cuts. Making the cut is great, but if you consistently finish near the bottom of the weekend leaderboard, you're probably not making us much money. So once a golfer made the cut, we wanted to know how often they turned that opportunity into a top-25 finish. This feature helped us separate the golfers who were simply surviving the cut from the golfers who were actually doing something with it.

#### Cost vs Consistency
At the end of the day, we still had a budget to work with. This feature helped us find the sleepers: golfers who were relatively inexpensive but consistently made cuts throughout the season.This was probably one of the most useful features we created because fantasy golf isn't just about finding good golfers. It's about finding good golfers who are worth what you're paying for them.

#### Results
We used these features along with our own intuition to make our final decisions. Looking back at the season, I'm happy to say that some of our best picks weren't chosen because of something we read on ESPN. They were chosen because the numbers made them interesting. Pierceson Coody, for example, was relatively cheap but had a high cut rate, making him exactly the kind of player we were looking for. He ended up being a great value pick that not many other teams had. Chris Gotterup was another example. He looked extremely undervalued based on the features we created, and he ended up winning three tournaments throughout the year.

Obviously, this doesn't mean our ratios predicted those wins. But they did exactly what we needed them to do: they helped us find players worth investigating that might have been overlooked by simply looking at rankings or salaries. 

### Conclusion
Overall, for our first year in the league, we did pretty solid. We held the number one spot for the entire year until we lost the last week (The FedEx Cup has such a big purse that if you don't have the winner you can't win the league). While it was disappointing to lose our crown after the whole year we still ended up 3rd of 17 teams. And more importantly, my grandpa constantly got calls from his friends wondering if we had cheated. 

From a statistical standpoint, this was one of my favorite projects because it reminded me that good analysis doesn't always have to mean a complicated model. I spend a lot of time learning increasingly complicated statistical methods, so my first instinct is often to figure out how I can use them. But sometimes the better question is:

What is the simplest way to answer the question we actually care about?

For us, that meant cleaning data from multiple sources, engineering features that captured consistency and value, and then using those features alongside our own golf knowledge to make decisions. And honestly, it worked pretty well.

That being said, I do have a reputation to uphold. Now that I have a little more time, I might have to try something more advanced for next season. But I wouldn't be surprised if this method holds up.

![Figure]({{site.url}}/{{site.baseurl}}/assets/img/golfrankings.jpeg)



