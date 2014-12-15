--- 
layout:     post
title:      "FS // My Third Web App - Ski Mountain Memories"
date:       2014-12-11 11:00:00
categories: flatironschool rails
tags:       ruby, rails, javascript, ajax, sql, postgres, heroku, instagram, html, css, geolocation
---

Partnering with [Jimmy Kuruvilla](https://github.com/JimmyKuruvilla) and [Blake DeBoer](https://github.com/blakedeboer), I created my final web application for the semester which we called "Ski Mountain Memories" (SMM).

### What does it do?

Based on hashtags, SMM can track any Instagram picture taken in the world as they happen and plot them on a map. The premise is this: you go with a group of friends, take IG pictures, and tag them with a specific hashtag. Every time anyone in the group does that, the picture gets picked up by our app in real-time and a marker is added onto a Google map based on the picture's geolocation. You can then view and share this map with anyone.

### Why the name "Ski Mountain Memories"?

The application's original intent was to track photos for groups of skiers/snowboarders. I'm a snowboarder and when I go boarding with a large group of people, we typically take pictures but don't know where they occurred on the mountain. Was it at the top? At the terrain park? Off a ramp somewhere? SMM was built to answer those questions.

### What's the tech stack?

- Ruby on Rails
- JavaScript & jQuery
- HTML/CSS & Bootstrap
- Postgres SQL
- Heroku
- Instagram API
- A handful of gems
  - New Relic: for error logging and tracking our app's performance
  - Unicorn: for handling multiple HTTP requests from IG
  - Figaro: for hiding ENV secrets
  - Friendly_id: for routing to pages by name

### What was your contribution to the project?

I added OAuth with Instagram (IG), set up sessions and ENV files with Figaro, and contributed heavily on the front-end. With Jimmy, we worked out a lot the controllers, including routing all the POST requests from IG and creating Visuals from the data sent. As a team, we designed all the models and db schema.

There's a lot that went into this project so I'm going to split up blog posts to cover individual pieces so I don't have one insanely long post. Keep a lookout for future posts.

### Takeaways from the project?

I took on a lot of the front-end work on this one because I spent most of my other projects on the backend. I thought this might help round my skills. Biggest takeway with that decision: I don't like front-end work. Well, I don't dislike it but every project I've been a part of at Flatiron has reaffirmed that I enjoy and prefer working on the backend. To me, it's just more fun to connect systems and generate data.
