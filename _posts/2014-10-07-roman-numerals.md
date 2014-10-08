---
layout: post
title:  "Recursive Roman Numerals"
date:   2014-10-07 22:15:03
categories: flatironschool, ruby
tags: arrays, hashes, recursion, classes, class methods, blocks, enumerables, iteration, sorting, data structures
---

So the `def` keyword is used to build `methods`...

...just kidding.

### Recursion, You Sexy Thing

Today, one of our labs consisted of adding a Class method `Integer#to_roman` which returns a string of Roman Numerals based on that integer. I got the specs to pass with the following code but I fully recognize that it is atrocious.

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

One of my teammates, [@Molly](https://github.com/molgin), finished early and seemed very pleased with her solution so I asked her to show me the code. Behold:

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

It's beautiful. 

It stores the roman numerals as key/value pairs; sorts and reverses them; calls find -- which returns the first key that evaluates to true -- then returns that key's value and recursively calls itself again after reducing the integer value. Once it gets to its base case, it returns an empty string and is complete. All on 10 lines!

I'll admit, when I read Molly's code, I felt like this scene out of Silicon Valley:

<img src="http://38.media.tumblr.com/125a0617d8986ad521772f0f42aa56db/tumblr_n68390DBXL1t9w6i8o1_500.gif" alt="Gilfoyle-Code-Gay">

Future post on `recursion` to come but I just wanted to shout out this sick chaining work of art.


