--- 
layout:     post
title:      "FS // First Tech Interview - Building Blackjack"
date:       2014-12-16 01:05:00
categories: interviews
tags:       ruby, blackjack, oop
---

I had my first technical interview over the weekend. The task was to build Blackjack. I started off a little nervous but thankfully, the interviewer ('M') was nice and the whole thing felt closer to pair programming than anything intimidating. 

At first, I wasn't sure where to start but after discussing the requirements, these were the questions I needed to answer:

- How do I represent the deck?
- How do I keep track of players?
- How do I deal cards?
- What decisions are made during Blackjack?
- How do we determine winners?

The first thing I tackled was generating the deck.

{% highlight ruby %}
def generate_deck
  num_cards = [2, 3, 4, 5, 6, 7, 8, 9] 
  face_cards = [10, 10, 10, 10, 11] # 10, J, Q, K, 11 represents Ace
  @deck = num_cards * 4
  deck += face_cards * 4
  deck.shuffle!
end
{% endhighlight %}

M gave me some leeway and allowed 11 to represent Aces (even though they can be 1 or 11). I wasn't 100% sure about shuffling an array or duplicating all its elements but when I said aloud "there is probably a method that does something like that", M's reply was, "Well, how would you check?". "Usually, I go to [Ruby OverAPI](http://overapi.com/ruby/) and test in IRB. Can I do that here?". He replied, "You sure can".

**fun fact #1:** multiplying an array by an integer n will duplicate that array n times. Like so:
{% highlight ruby %}
[1,2,3] * 3    #=> [1,2,3,1,2,3,1,2,3]
{% endhighlight %}

Once I built the deck, I needed to be able to deal the cards. My first thought was to `sample` but M said that would be randomly picking from the array without removing a card. He nudged me towards `shift` since dealing cards in real life requires taking them off the top of a deck (`pop` works too).

Then I sat for a minute wondering, "How do I 'hold onto' the cards?". I was trying to do too much within the method and M suggested object-oriented design. That's when I switched gears and built a `Game` and a `Player` class.

{% highlight ruby %}
class Player
  attr_accessor :hand

  def initialize(player_number)
    @hand = []
  end
end

class Game
  attr_accessor :players

  def initialize(num_players)
    @players = []
    generate_deck
  end
end
{% endhighlight %}

Then I built these two methods in conjunction of each other:

{% highlight ruby %}
# for Player
def receive_card(card)
  hand << card
end

# for Game
def deal_cards
  2.times do
    players.each { |player| player.receive_card(deck.shift) }
  end
end
{% endhighlight %}

`#receive_card` keeps track of cards in a Player's hand while `#deal_cards` goes around the "table" and deals a card one by one in a round-robin fashion. Each player gets two cards, hence, `2.times do`

Once I got into the mindset of building objects, things started flowing. I kept methods small and tried to maintain separation of concerns. When we got to determining player action, he lightened the rules to "a player will hit if their hand is < 15". There are more complicated rules to Blackjack but I'm betting M wanted to make sure I finished.

So I built these methods:

{% highlight ruby %}
# for Player
def hit?
  sum = 0
  hand.each {|card| sum += card}
  sum < 15 ? true : false
end

# for Game
def play
  players.each do |player|
    while player.hit?
      player.receive_card(deck.shift)
    end
  end
end
{% endhighlight %}

For `#hit?`, before I summed the hand with the `each` method, I verbalized that there was method that summed an array. I took a quick look at OverAPI but M said there wasn't a method to do that so I didn't linger on it and continued with the `each` method. 

**fun fact #2:** You can sum an array of ints with `reduce(:+)`. This is what I remembered.

As for `#play`, here I wanted to go through each player and have them draw as many cards as necessary to get above 15.

Lastly, I had to determine winners. So I wrote something like this:

{% highlight ruby %}
# for Player
def hand_value
  sum = 0
  hand.each {|card| sum += card}
  sum
end

# for Game
def determine_winners
  eligible_winners = players.select{ |player| player.hand_value <= 21 }
  winning_score = eligible_winners.collect{ |player| player.hand_value}.sort.last
  winners = players.select {|player| player.hand_value == winning_score }
end 
{% endhighlight %}

The idea is to find all the players who have a hand_value of less than 21. Then find the largest value of all hands and return only the players with hands of that score (since multiple winners can win in blackjack).

M was happy enough with this and decided to end the interview there since we only had about 5 minutes left for questions. He said I did well and that I got into a rhythm once I started moving towards OOP. Some takeways from my interview with him were:

1. It's okay to test code in IRB or check online resources during an interview (should clarify with interviewer first)
2. Object-oriented programming is *usually* better for interviewing because it displays specific actions and tends to showcase a person's thought process. 
3. Check-in on assumptions and clarify any questions that arise. It helps the interviewer steer you in the right direction and stop you from going down the wrong path.
4. Tech interviews are nerve wracking but the more you talk it out and the more code you put on paper, the easier it gets. Plus, having a back and forth experience is 1000% better than a silent coding session; for both parties.

In case you were wondering, this code is not 100% perfect and will break. I later went back, cleaned up my code, and changed the results to display all outcomes so that winners and losers are more evident.

Below is a better version of my simple Blackjack game. *Note*: it is still simple and does not encapsulate the finer strategic moves of the game. I could also separate objects even more with a Card or Deck class but for a one hour interview and another hour following up, plus 2-3 hours to blog about it, I'm happy to conclude it here.

Finished version:

{% highlight ruby %}
class Player
  attr_accessor :hand, :id

  def initialize(player_number)
    @hand = []
    @id = player_number
  end

  def receive_card(card)
    hand << card
  end

  def hand_value
    hand.reduce(:+)
  end

  def hit?
    hand_value < 15 ? true : false
  end
end
{% endhighlight %}

{% highlight ruby %}
class Game
  attr_accessor :players, :deck

  def initialize(num_players)
    @players = []
    add_players(num_players)
    generate_deck
    deal_cards
  end

  def add_players(num_players)
    num_players.times { |idx| players << Player.new(idx + 1) }
    players << Player.new(players.length + 1)  # Dealer
  end

  def generate_deck
    cards = [2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10, 11] #11 represents Ace
    @deck = cards * 4 
    deck.shuffle!
  end

  def deal_cards
    2.times do
      players.each { |player| player.receive_card(deck.shift) }    
    end
  end

  def play
    players.each do |player|
      while player.hit?
        player.receive_card(deck.shift)
      end
    end

    determine_winners
  end

  def determine_winners
    dealer_hand = players.pop.hand_value
    p "Dealer has #{dealer_hand}"

    players.each do |player|
      if player.hand_value <= 21
        if player.hand_value > dealer_hand
          p "Player #{player.id} wins with #{player.hand_value}"
        elsif player.hand_value == dealer_hand
          p "Player #{player.id} pushes with dealer"
        else
          p "Player #{player.id} loses with #{player.hand_value}"
        end
      else
          p "Player #{player.id} busts with #{player.hand_value}"
      end
    end
  end
end
{% endhighlight %}

With `Game.new(3).play`, example result is:
{% highlight bash %}
"Dealer has 16"
"Player 1 pushes with dealer"
"Player 2 loses with 15"
"Player 3 wins with 19"
{% endhighlight %}