---
layout: post
title:  "FS // Day 6 | Object Orientation"
date:   2014-10-06 22:15:03
categories: flatironschool ruby oo
tags: hashes, recursion, classes, class methods, blocks, enumerables, iteration, sorting, data structures, object-orientation, oo, xerox, apple, xparc pirates, alan kay
---

So the `def` keyword is used to build `methods`...

...just kidding.

### Biggest Problem of the Day (BPD): Roman Numerals 

Task: Write an Integer Class method that returns a string of Roman Numerals based on its integer.

I got the specs to pass with the following code but I fully recognize that it is atrocious and not what anyone would consider `DRY`.

{% highlight ruby %}
class Integer
  def to_roman
    numerals = []
    number = self
    while number > 0
      if number >= 1000
        numerals << "M"
        number -= 1000
      elsif number >= 900
        numerals << "CM"
        number -= 900
      elsif number >= 500
        numerals << "D"
        number -= 500
      elsif number >= 400
        numerals << "CD"
        number -= 400
      elsif number >= 100
        numerals << "C"
        number -= 100
      elsif number >= 90
        numerals << "XC"
        number -= 90
      elsif number >= 50 
        numerals << "L"
        number -= 50
      elsif number >= 40
        numerals << "XL"
        number -= 40
      elsif number >= 10
        numerals << "X"
        number -= 10
      elsif number >= 9
        numerals << "IX"
        number -= 9
      elsif number >= 5
        numerals << "V"
        number -= 5
      elsif number == 4
        numerals << "IV"
        number -= 4
      elsif number < 4
        numerals << "I"
        number -= 1 
      end
    end
    numerals.join("")
  end
end
{% endhighlight %}

One of my teammates, [@Molly](https://github.com/molgin), finished early and seemed very pleased with her solution so I asked her to show me the code. Behold.

{% highlight ruby %}
class Integer
  def to_roman
    rom_key = { 1000 => "M", 900 => "CM", 500 => "D", 400 => "CD", 100 => "C", 90 => "XC",
      50 => "L", 40 => "XL", 10 => "X", 9 => "IX", 5 => "V", 4 => "IV", 1 => "I"
    }
    return "" if self == 0
    key = rom_key.keys.sort.reverse.find{ |key| self >= key}        
    return rom_key[key] + (self - key).to_roman
  end
end
{% endhighlight %}

Recursion, you sexy thing.

Let's break this down:

* It stores the roman numerals as key/value pairs
* sorts and reverses the hash so that all the largest numbers come first
* calls find -- which returns the first key that evaluates to true -- in this case, the largest number closest to the integer
* returns that key's value -- a roman numeral string
* and then recursively calls itself again after reducing the integer value by the hash value. Once it gets to its base case, it returns an empty string and is complete. 

All on 10 lines!

I'll admit, when I read Molly's code, I felt like this scene out of Silicon Valley:

<img src="http://38.media.tumblr.com/125a0617d8986ad521772f0f42aa56db/tumblr_n68390DBXL1t9w6i8o1_500.gif" alt="Gilfoyle-Code-Gay">

Future post on `recursion` to come but I just wanted to shout out this sick chaining work of art.

### Rest of the day:
The start of lecture was about the Xparc Pirates. Basically, in the late 70's, Xerox was the epicenter of technology advancement: they created object orientation, pointers, the mouse, the GUI -- all brought on by [Alan Kay](http://en.wikipedia.org/wiki/Alan_Kay) and his team. But in 1979, they were forced by Xerox executives to show off their creations to Steve Jobs and Apple who basically stole everything. Months after the visit, Apple delivered their iconic Macintosh and became one of the most valuable technology companies in the world. Xerox on the other hand, would be relegated and only known for its... printers.

### Object Orientation
We finally jumped into object orientation (OO)! Objects are anything that encapsulate data. Integers, Strings, Arrays, Hashes, Classes... everything in Ruby is an object. We discussed Classes, class methods, instance methods, initializing object attributes with `def initialize`, setters & getters/writers & readers, and `attr_accessor`, `attr_reader`, `attr_writer`. 

Here is a very simple `Class` we built:

{% highlight ruby %}
class Book
  attr_accessor :author, :page_count
  attr_reader :title, :genre

  GENRES = []

  def initialize(title)
    @title = title
  end

  def genre=(genre)
    @genre = genre
    GENRES << genre
  end

  def turn_page
    puts "Flipping the page...wow, you read fast!"
  end
end
{% endhighlight %}

I'm learning a ton and it's just baffling to see how far I've come in the last 8 days. Avi is a phenomenal teacher and working with other students, bouncing ideas and fielding each other's questions, has *exponentially* increased my learning. I'm loving it.

Left FS @9pm

