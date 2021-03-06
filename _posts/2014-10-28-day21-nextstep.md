---
layout: post
title:  "FS // Day 21 | My First Web App - NextStep"
date:   2014-10-28 11:30:30
categories: flatironschool nextstep
tags: ruby, watir-webdriver, nokogiri, sinatra, scraping, erb, web app, testing, html, css, front-end, api
---

# Who's going to hire me when I graduate? 

It must be the old recruiter in me but this is the question I've been asking myself ever since I started studying at Flatiron School. Over the last three days, I and another student built the answer to that question. We call it NextStep, and earlier this evening, we had the opportunity to debut it at Flatiron Presents. Here's a video: 

<iframe src="https://docs.google.com/file/d/0B2BGZJ-jbmLncW12aG5UcTlLTnM/preview" width="640" height="400"></iframe>

A lot of folks told me I did a great job and had nice things to say about our presentation. It was an awesome and humbling experience filled with wonderful emotions and a couple of 'firsts'. 

#### NextStep is the first app I ever truly built.

Not designed from a CS50/6001x Pset or Codecademy tutorial; not from a Code School walkthrough or Odin Project assignment; but from my own mind. It's a beautiful feeling - to be able to create something from nothing - to start putting down code on a blank Sublime sheet of "paper" and have it become this thing capable of connecting systems, scraping and aggregating data, and presenting it all back in pretty charts and graphs.

It was also my first technical presentation. I've been to my fair share of tech talks and it's always interesting to watch someone stand up and show off something cool they built. Now I've done it too! 

#### Here are a couple of things I'm thankful for:

1. My awesome partner. Vaidehi and I probably spent 30 hours (each) working on NextStep. She really helped me out on the front-end working with Google's Maps API and Charts libraries. Without her, I would've only had boring text data to display and talk about; which is a funny thing actually. Prior to starting FS, I thought I was more interested in front-end & design but what really excited on this project was getting the systems to interact correctly and making sure I got the data. I'll refrain from saying I might be a backend guy because I don't know if that's true yet. I'm still learning.
2. My college years. Spending the majority of those years performing on stage and in shows made it so that I was almost 0% nervous for my tech talk. Vaidehi and I also practiced a handful of times which made for a smoother flow.
3. the open-source community. I leveraged a ton of Ruby gems to make this magic happen and without their generosity, I just wouldn't have been able to do this.
4. My ERB post. Writing that post and learning to implement ERB really carried over to this project.

#### Lessons Learned

As I mentioned, I spent over 30 hours on NextStep. The first six hours on Saturday were spent experimenting with different gems like Capybara, Poltergeist, and Mechanize (with no success). Tristan pointed me in the direction of using Poltergeist to fake a browser header but I kept getting denied access when trying to connect to LinkedIn, as well as Twitter, Reddit, and most other sites. The documentation for Capybara wasn't leading me in the right direciton either so eventually I abandoned it altogether.

I also gave Mechanize a try after hearing about it through another student's blog. At first, it seemed promising but about an hour in I realized it didn't play well with JavaScript so I had to scrap that gem too. It wasn't until I found Watir-Webdriver that I was finally able to open a browser and interact with LinkedIn via command line. It was *so simple*. A++ for Watir's concise and effective documentation. "It just works"!

Scraping is hard. I mean, yes, it's easy with Nokogiri but it's also a lot of work identifying all the rights nodes in an HTML doc and formatting that data - especially if you're working with a bunch of different pages. Okay, maybe hard isn't the right word; time-consuming.

Github is amazing. I know we use it in class to pull and push repos but it wasn't until this project that I finally saw its real value. Vaidehi and I still made mistakes like pushing directly to master each time but being able to see our logs and reset back to a point where we knew our system was stable was so clutch.

Sidenote, resetting the head without committing updated code is horrifying. I lost 4 hours of working on a geocoding feature from last night. When this morning came around, I forgot to commit and just reset back to the point of safe demo, and *poof*...code all gone. 

Anyhow, I'm very happy with how everything turned out. I can't believe it's only been 21 days and I'm amazed at how much I've learned. We still haven't even touched on Rails! I'm going to optimize the app and familiarize myself more with the libraries & APIs we used. It's also time to get back to work on the labs that I had been putting off. 

All in all, it was a great Tuesday evening.

