---
layout: post
title:  "FS // Day 8 | Web Scraping & MVC"
date:   2014-10-10 01:30:30
categories: flatironschool ruby oo mvc
tags: classes, class methods, instances, instance methods, writers, readers, setters, getters, hashes, arrays, object-orientation, oo, scraping, mvc, perl, larry wall
---
#### “The three chief virtues of a programmer are: laziness, impatience, and hubris.” - Larry Wall

### Biggest Problem of the Day: Student Site Scraper

Task: Build a Command Line Interface (CLI) that can list and display data from the Ruby class student website

Two days ago, we did something really fun. We did our first "team" lab where we all had to work together to build a CLI that could scrape data from the student website and perform certain actions based on user input; things like list students; display a student's individual web page, Github page, Twitter site, etc. This lab started teaching us how to interact with website data; using gems like Nokogiri, Open-URI, and Bundler; splitting our classes and functionality into separate directories (bin/lib/config); and working together while simultaneously building separate pieces of a program.

It was an interesting experience. I honestly wrote the least amount of code and played more of the Product Manager role making sure my teammates knew what they were responsible for and connecting the pieces at the end. Molly worked on the scraping functionality and Sarah built the CLI. I mostly assisted Sarah or cleaned up code whenever one of them pushed to the repo.

Here's a snippet of the scraper:

{% highlight ruby %}
def create_hash_of_students
  students_hash = {}
  url = 'http://ruby006.students.flatironschool.com/'
  html = open(url)
  student_dir = Nokogiri::HTML(html)
  students = student_dir.css("li.home-blog-post")
  students.each do |student|
    name = student.css("div.big-comment h3 a").text
    students_hash[name] = {}
    students_hash[name][:front_tagline] = student.css("p.home-blog-post-meta").text
    student_page_url = url + student.css("div.big-comment h3 a").attribute("href").to_s
    students_hash[name][:url] = student_page_url
    # ...
  # ...end
{% endhighlight %}

One of the CLI methods

{% highlight ruby %}
def list_students(list_of_students)
  list_of_students.each_with_index {|name, idx| puts "Student ##{idx+1}. #{name}"
end
{% endhighlight %}

I felt like this lab gave me a preview into what working with other programmers would be like IRL. Molly is easily one of, if not the, best student in the class. She just "gets it" and plows through labs like it's nobody's business. But I also noticed that she is very particular about her code and if things don't work the way she thought it would, she'll go chasing down a rabbit hole trying to figure out why. This is actually a good trait in a programmer and would be perfectly fine if she were building the program on her own but Sarah's CLI needed the dataset that Molly's scraper would return and, on more than a few occasions, I had to ask Molly to push her working code so that Sarah could work with real data. Other than that, I got out of Molly's way and let her scrape that site to shreds. Foreshadowing?

### Lecture & Programmer of the Day: Larry Wall
[Larry Wall](http://en.wikipedia.org/wiki/Larry_Wall) is the creator of Perl which Matz credits as being a major influence on Ruby. Larry also has a hilarious [website](http://webcache.googleusercontent.com/search?q=cache:TgceZi5SMqAJ:www.wall.org/~larry/+&cd=1&hl=en&ct=clnk&gl=us) that is so bad it has to be on purpose. His wit is evident with his remark about chartreuse.

In lecture, Avi went over the Student Scraper lab and very lightly introduced the concept of Model-View-Controller. He discussed separating our program into 3 main objects; three separate classes: a Student Class (Model), a StudentScraper, and a StudentCLI (Controller) (no view because we were using a CLI). He was doing his own foreshadowing with re. to Rails and how a program's file structure should be separated. I felt like I developed a stronger understanding of the config/environment file in this review. I liken it to using a CSS file when building HTML pages (you only have to change something in one file to change the rest).

### Fun part: group changes
We switched up groups today; which I'm happy about. There are 40 students in the class and it's hard to meet all of them when the entire day is spent on labs and lecture. Switching is necessary to meet new faces. I didn't lose the whole squad as Josh traveled with me and now we're working with Vaidehi, an ex-teacher/writer, and Julie who is a Comp Sci grad from Bard. 

A few of us finished labs "early" so I ended the day watching music videos and hip hop and modern dance choreo with Thinh, which was great. I left at 7pm and it's just funny that I now consider a 10 hour day "early".

Left FS @7pm.
