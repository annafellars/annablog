---
layout: post
title:  "Fantasy Football Statistics"
date: 2024-09-30
description: How to use R to run a simple analysis to improve your fantasy football picks.   
image: "/assets/img/football.jpg"
---

<p class="intro"><span class="dropcap">F</span>antasy Football is in full swing and after a hard loss to my 10-year-old cousin, I realized I needed to step up my game. Luckily, I realized I have a big advantage: I’m a statistics major! I spent the last week researching the best metrics and data sources and now I’m sharing with you how I improved my Fantasy Football team and how you can too!</p>

![Figure]/assets/img/image_name.jpg)

### How Fantasy Football Works

To start let’s make sure we’re all on the same page for how Fantasy Football works. I play in an ESPN league although there are several other websites you can play on. Essentially, you can have up to 17 NFL players on your roster with 9 players as your starters. Each week you are matched up with another fantasy team and as your starters play in their real-life games, they earn points for your fantasy team. At the end of the week, whichever fantasy team has the most points wins that match-up. 

The points are made up of many different components based on a player's position. Here is how ESPN calculates the main points.

![Figure](/assets/img/ff_scoring.jpg)

With so many factors adding up to how points are earned, it's nearly impossible to separate the signal from the noise when predicting fantasy football along with any other sports analytics. That being said, I had to take a look for myself as the app-provided stats were leading me astray. I have broken this process down into 3 steps of how you can start your own fantasy football analysis. 

### Step 1: Gather Your Data
There are many different sources on the internet to collect data, many people even have dedicated websites to collecting football stats. After researching, I decided to go with a fantasy football R package called “ffopportunity”. This package scrapes the most updated data from NFL play-by-play data and builds a data frame of Expected Fantasy Points by applying an xg-boost model.  

Once I installed the “ffoportunity” package, it was easy to upload the data. The data splits into 3 tibbles, one for an overall player summary, one focused on passing yards, and the last on rushing yards. I took each one and changed it to a data frame. Here’s what the passing yards dataframe looks like. 

![Figure](/assets/img/pass_plays.jpg)

### Step 2: Choose Your Metrics
The next step is separating the signal from the noise. As I mentioned before, if it was easy to predict fantasy points, there would be no point in playing. As such there are already hundreds of models and ideas for what works best. After lots and lots of research, I decided to start my analysis with air yards to keep it simple.

AIR YARDS: From the multiple websites and models I looked at, air yards are always very correlated with fantasy points. Air yards measure how far the football travels in the air past the line of scrimmage - both incomplete and complete passes are included. This mostly applies to quarterbacks, but wide receivers also get a few points to their name. To look at this metric I used ggplots to created a scatterplot to get a better look. 

![Figure](/assets/img/first.jpg)

This graph is really messy. Each point is an individual pass and there is so much data it’s hard to make anything out. I colored it by if the pass was incomplete or not in hopes that it would show a clearer trend, but as you can see it is still very messy. 

I knew I needed to do some data engineering to get more from this data. I decided to start by grouping by quarterback so instead of 3,000+ data points, I was left with 49. This also meant I needed to sum together the air yards, completed passes, and expected fantasy points. Because I still wanted to see the points earned from incomplete passes, I changed completed passes to be a numeric value instead of a factor; this way I could still add up the passes without filtering out information from rows with incomplete passes. Once I did this and added a few things for aesthetics, it was easy to see that there is a very positive trend between air yards and points. 

There is also a very strong trend between complete passes and points. As straightforward as this seems, you need to choose players that have more playing time even if they aren’t as good because they will have more opportunities. In fantasy football terms “volume is king”.

![Figure](/assets/img/qb_graph.jpg)

I next grouped my data by game to see if it was still relevant in an individual game as if you want to win a weekly match up, you need your players to do good in each game, not just in their overall season. As you can see below the trend is still there in both air yards and completed passes per game. 

![Figure](/assets/img/game_graph.jpg)

Last, although the graphs are great I wanted to be sure there is a correlation between air yards, complete passes, and expected points. I ran Kendall’s Tau Correlation Test to get actual values.

![Figure](/assets/img/corr_ay.jpg)   
![Figure](/assets/img/corr_cp.jpg)

Although both air yards and complete passes have a statistically significant correlation with expected points, complete passes have a much stronger correlation than air yards. This surprised me as all my prior reading told me air yards are what you want to look at.

### Step 3: Apply the Analysis to Your Roster
Now that I have an idea of how these metrics apply to fantasy points, it’s time to update my roster. Unfortunately since many players are already spoken for, its not as simple as finding the players with the best metrics. But I used what I learned to move players around on my roster and have a few players that I’ll be watching for future trades. Here’s how my roster ended up doing:

![Figure](/assets/img/image_name.jpg)

### Conclusion
Here is where I will finish my conclusion

#### Helpful Resources
[ffopportunity](https://ffopportunity.ffverse.com/index.html) - the R package I used in this post

[ffanalytics](https://fantasyfootballanalytics.net/2016/06/ffanalytics-r-package-fantasy-football-data-analysis.html) - another R package for downloading data

[Air Yards](https://airyards.com/wopr.html) - a cool website that looks at Air Yard Metrics

[Advanced Stats](https://www.youtube.com/watch?v=I5C7ZGA6KSA) - a youtube video of some unique stats to look at for fantasy football
