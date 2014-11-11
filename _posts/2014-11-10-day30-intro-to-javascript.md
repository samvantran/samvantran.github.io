--- 
layout:     post
title:      "FS // Day 30 | Intro to JavaScript"
date:       2014-11-10 11:08:00
categories: flatironschool javascript
tags:       javascript
---

Today, we kicked off the first day of what will be our week-long adventure with JavaScript. We quickly (and broadly) covered the basics of JS and how it is different from Ruby.

### Here are 10 notable differences between the two:

1. The `var` keyword is required for declaring variables.
2. Curly braces `{}` start and end functions and blocks.
3. Semi-colons `;` end all statements and expressions.
4. Explicit `return` statements must used inside of functions/blocks otherwise `undefined` will be returned. This is different from Ruby's last-line implicit return. Here's a classic example that showcases numbers 1-4:

{% highlight javascript %}
var fizzbuzz = function(num) {        // declare variables with var
  if( num % 5 === 0 && num % 3 === 0 ) { 
    return "FizzBuzz";
  } else if( num % 5 === 0 ) {        // curly braces open/close blocks
    return "Buzz";
  } else if (num % 3 === 0 ) {
    return "Fizz";                    // end statements with ';'
  } else {
    return num;                       // use explicit return
  }
};
{% endhighlight %}

###### Below is actually #5. It looks like a numbered list will restart if a code block is inserted within. Must be a Markdown 'bug'. 
5. The Window object represents the global scope. Declaring a function creates a new scope within itself. 
  * Note: Within a function, the var keyword must be used when declaring new variables otherwise they become global variables. This is because Window is the implicit object. 
  * Note #2: Do not create global variables.
6. Functions are first-class objects and can be passed as arguments within other functions.
7. There are *a lot* of falsey values in JS:
  * Falsy values in Ruby: `false, nil`
  * Falsy values in JS: `false, null, undefined, 0, NaN, "" (empty string)`
8. Arity checking. Ruby enforces the number of arguments required when initializing a class object. Not so in JS. You can have any number of arguments. Any that aren't accounted for will have a value of undefined.
9. `If else` blocks do not require an `end`.
10. Instance Methods vs. Prototype Properties.
  * In Ruby, you define all instance methods within a class definition. In JS, you can do the equivalent by attaching them as properties to the Object.prototype. This lets you add as many "methods" as you want to a Ruby function. See example:

{% highlight ruby %}
# Ruby version
class Person
  def initialize(name)
    @name = name
  end

  def sayHello
    "Hi, I'm #{@name}. Nice to meet you!"
  end
end
{% endhighlight %}

{% highlight js %}
// JavaScript version
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
    return "Hi, I'm " + this.name + ". Nice to meet you!";
}
{% endhighlight %}

Tomorrow, we'll be learning about Closures and other voodoo magicks. 


