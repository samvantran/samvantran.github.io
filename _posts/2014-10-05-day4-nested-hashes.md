---
layout: post
title:  "FS // Day 4 | Feelings Friday"
date:   2014-10-05 21:15:03
categories: flatironschool ruby
tags: arrays, hashes, regex, yield, blocks, enumerables, iteration, sorting, data structures, nested data structures, collections, named parameters, grace hopper
---
##### writing this post Sunday evening after coming in at 1pm for tutoring and to continue working on labs.

### Biggest Problem of the Day (BPD): NYC Pigeon Organizer

Task: Organize a nested hash of NYC pigeon data

There were a lot of challenging labs but I felt like this one taught me the most with re: to nested hashes. We basically had to take this hash: 

{% highlight ruby %}
pigeon_data = {
  :color => {
    :purple => ["Theo", "Peter Jr.", "Lucky"],
    :grey => ["Theo", "Peter Jr.", "Ms .K"],
    :white => ["Queenie", "Andrew", "Ms .K", "Alex"],
    :brown => ["Queenie", "Alex"]
  },
  :gender => {
    :male => ["Alex", "Theo", "Peter Jr.", "Andrew", "Lucky"],
    :female => ["Queenie", "Ms .K"]
  },
  :lives => {
    "Subway" => ["Theo", "Queenie"],
    "Central Park" => ["Alex", "Ms .K", "Lucky"],
    "Library" => ["Peter Jr."],
    "City Hall" => ["Andrew"]
  }
}
{% endhighlight %}
 
and organize the data into a new hash that listed each pigeon name with their respecitve attributes. Like so: 

{% highlight ruby %}
pigeon_list = {
  "Theo" => {
    :color => ["purple", "grey"],
    :gender => "male",
    :lives => "Subway"
  },
{% endhighlight %}

This one took a lot of experimenting with IRB. I had to solidify my understanding of hashes; accessing keys and values; adding hashes into hashes; etc. 

This is what I came up with: 

{% highlight ruby %}
def nyc_pigeon_organizer(pigeon_data)
  organized_pigeon_data = {}

  pigeon_data.each do |classification, type|
    type.each do |attribute, pigeons|
      pigeons.each do |pigeon|  
        if organized_pigeon_data[pigeon] == nil
          organized_pigeon_data[pigeon] = { classification => attribute.to_s }
        elsif organized_pigeon_data[pigeon][classification] == nil
          organized_pigeon_data[pigeon][classification] = attribute.to_s
        else          
          organized_pigeon_data[pigeon][classification] = [ organized_pigeon_data[pigeon][classification] ] << attribute.to_s
        end
      end
    end
  end
  organized_pigeon_data
end
{% endhighlight %}


Big takeaway: `hsh[:key] = value` assigns a pair within the hsh but if that `:key` already exists, and you want to instead store multiple values into an array, you have to 

`hsh[:key] = [ hsh[:key] ] << value`.

Oh, I'm also glad that I strengthened my understanding of Regexs thanks to the Tweet Shortner and Essay Generator labs. 

Need to find a citation like "(Tran, 2014)"? Use this bad boy: `/\W[a-z]+\W \d\W/i`

### Rest of the day
Friday's lecture discussed [Grace Hopper](http://en.wikipedia.org/wiki/Grace_Hopper) who invented the first compiler, COBOL, and was the one who coined the term ["debugging"](http://en.wikipedia.org/wiki/Grace_Hopper#Anecdotes). We also dove into Ruby hashes, symboles, yield, blocks, and built our own `.each` and `.collect` methods. 

Then we had Feelings Friday! This was an interesting and enjoyable experience. We all sat in a huge circle and one by one we expressed how felt about the week. It was unadulterated, uninterrupted, and it offered each student the opportunity to speak their mind with no judgments. 

The general consensus was that we're all highly motivated; we feel challenged (and sometimes overwhelmed); that everyone else is nice and helpful (without being arrogant); that time passes incredibly fast; that we're all working together to reach the same destination.  Some students expressed despair in their previous jobs or that life simply seemed bleak with no sense of purpose and that being at Flatiron School has completely changed their lives.

Avi said something that resonated well with me. While there isn't a competition amongst students, some do feel like they're behind or slower than others. Avi compared FS to running a marathon and that the only thing students should focus on is learning as much as possible and moving at their own pace. A common saying for runners is, "My race, my pace".

Personally, I'm very thankful and happy to be in this type of environment again. I feel like I'm drinking from a firehose again with the sheer amount of information I'm learning every day. Being surrounded by other smart, motivated, and friendly people also makes this a great experience.

Left @8:45pm.







