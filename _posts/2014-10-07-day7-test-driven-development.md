---
layout: post
title:  "FS // Day 7 | Test-Driven Development"
date:   2014-10-07 22:30:30
categories: flatironschool ruby oo
tags: classes, class methods, blocks, enumerables, iteration, sorting, data structures, object-orientation, oo, test-driven development, tdd, kent beck, hip-hop, dancing
---
#### "Make it work, make it right, make it fast" - Kent Beck

### Funnest Problem of the Day: Emoticon Translator

Task: Take a YAML file full of emoticons and write a translator that can determine the english equivalent or its meaning based on the japanese emoticon.

This lab was fun. We learned to use `File.read` a file's contents and use the YAML `gem` to parse the data and return a nicely composed hash. This was the emoticon file:

{% highlight yaml %}
angel:
  - "O:)"      
  - "☜(⌒▽⌒)☞"
angry:
  - ">:("
  - "ヽ(ｏ`皿′ｏ)ﾉ"
bored:
  - ":O"
  - "(ΘεΘ;)"
confused:
  - "%)"
  - "(゜.゜)"
embarrased:
  - ":$" 
  - "(#^.^#)"
fish:
  - "><>"
  - ">゜))))彡"
glasses:
  - "8D"
  - "(^0_0^)"
grinning:
  - "=D"
  - "(￣ー￣)"
happy:
  - ":)"
  - "(＾ｖ＾)"
kiss:
  - ":*"
  - "(*^3^)/~☆"
sad:
  - ":'("
  - "(Ｔ▽Ｔ)"
surprised:
  - ":o"
  - "o_O"
wink:
  - ";)"
  - "(^_-)"
{% endhighlight %}

And this was my finished code :) ... no wait, I mean this (＾ｖ＾)

{% highlight ruby %}
# require modules here
require 'yaml'
require 'pry'

def load_library(file_path)
  file = File.read(file_path)
  emoticons = YAML.load(file)
end

def get_japanese_emoticon(file_path, emoticon)
  emoticons = load_library(file_path)
  emoji = emoticons.values.find {|faces| faces[0] == emoticon}
  emoji == nil ? "Sorry, that emoticon was not found" : emoji[1]
end

def get_english_meaning(file_path, emoticon)
  emoticons = load_library(file_path)
  emoji = emoticons.find {|name, faces| faces[1] == emoticon }
  emoji == nil ? "Sorry, that emoticon was not found" : emoji[0]
end
{% endhighlight %}

I have to say, I *really* like using ternary operators. There's just something about them that makes me happy whenever I get to throw down the `? true : false` scenario.

Also, special shoutout to `pry` for being a really awesome debugging tool. I know it can do way more than that but so far, I've used it to understand how my code is operating and troubleshoot any issues that arise. It's great. However, I do wish it had the ability to iterate and execute lines of code in run-time like C's GDB. I was told pry-debug is another gem that has that type of feature. (Note to self: look into that).

### Lecture & Programmer of the Day: Kent Beck
[Kent Beck](http://en.wikipedia.org/wiki/Kent_Beck) is credited as being the father of Test-Driven Development (TDD) and Extreme Programming (XP). He was one of the leaders to pioneer the Agile methodology for programming. I put one of his biggest quotes at the top because I really like the sound of it. IMO, it captures the essence of good programming. Plus, Avi says you have to make sure a program works before you can optimize i.e. "you can't optimize bad code". 

### Fun part: hip-hop dancing
We did some hip-hop dancing today. Personally, I **love** hip hop choreo and dance. It's one of my favorite things to do, ever. I was really excited for this but unfortunately, it was not as great as I had hoped. I have no doubt the teacher is an excellent dancer but I felt like his teaching was lackluster with really *really* old and outdated music and "dance moves". FWIW, I also recognize that the majority of the class does not enjoy dancing as much as I do.

BUT! I don't want to end this post on a low note so here's a video Avi played for us at the start of lecture. It's The Company performing at Vibe XIX this year (when he put this up, I was like "Oh I know this!!!"). Super awesome choreo!!

<iframe width="600" height="400" src="//www.youtube.com/embed/zY2D0j454PI" frameborder="0" allowfullscreen>Your browser does not support this video</iframe>

Left FS @7:15pm.
