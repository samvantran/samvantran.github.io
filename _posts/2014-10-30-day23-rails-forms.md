---
layout: post
title:  "FS // Day 23 | Rails - ActionView Forms"
date:   2014-10-30 11:30:30
categories: flatironschool ruby rails
tags: ruby, rails, form, formhelpers
---

Today we learned about forms, specifically, ActionView's FormTagHelper and FormHelper. 

* FormTagHelper (form_tag) is a shortcut to HTML form fields but require explicit validations.
* FormHelper (form_for) is smart, knows of resources, and has validations for an object.

Both are Rails helpers that automagically build forms and free you from having to hardcode a lot of HTML. They also name and pre-fill certain attributes based on Rails naming conventions. 

On this page, I'll be covering FormHelper a la `form_for`.

### CRUD

Forms enable CRUD actions depending on the type of object in scope. Notably, form helpers will automatically know to set up the following actions:

* GET (index/show/edit/new)
* POST (create)
* PATCH (update) and
* DELETE (destroy)

### Three steps to making forms work

* make sure routes are configured
* make sure controllers know what to do
* make sure views handle objects appropriately

### Breakdown

* make sure routes are configured; inside routes.rb

`resources :lists` or `get '/lists' => 'lists#index'`

* make sure controllers know what to do

{% highlight ruby %}
def create
     @list = List.find(params[:list_id])
     @item = @list.items.build(items_param)
     @item.save

     redirect_to list_path(@list)
end

private
  def items_param
     params.require(:item).permit(:description)
  end
{% endhighlight %}

 * make sure forms and views handle objects appropriately. 

{% highlight erb %}
  
<%= form_for([@list, Item.new]) do |f| %>
 <%= f.text_field :id => “new-todo”, :placeholder => “Add task” %>
<% end %>

{% endhighlight %}

Below is a list of the different form_for helpers:

* check_box
* collection_check_boxes
* color
* date
* datetime
* email
* fields_for
* file_field
* forms_for
* label
* month
* number
* password
* phone
* radio_button
* range
* search
* text_area
* text_field
* time_field
* url
* week 

Included below is the ERB code (and html that is generated). HTML is commented out:

{% highlight erb %}
:)
  <%= f.label :check_box %><br>
  <%= f.check_box :user_id %><br>
  <!-- <input id="post_user_id" name="post[user_id]" type="checkbox" value="1"> -->

  <%= f.label :collection_boxes %><br> <-- generates input and label tags -->
  <%= f.collection_check_boxes :user_id, User.all, :id, :name %><br>
  <!-- <input id="post_user_id_1" name="post[user_id][]" type="checkbox" value="1">
       <label for="post_user_id_1">Crookshanks</label> -->
  
  <%= f.label :color %><br>
  <%= f.color_field :color, :value => "#abcdef" %><br>
  <!-- <input id="car_color" name="car[color]" type="color" value="#000000" /> -->
  
  <%= f.label :date %><br>
  <%= f.date_field(:content, :value=> "1990-01-01") %><br>
  <!-- <input id="user_born_on" name="user[born_on]" type="date" /> -->

  <%= f.label :datetime %><br>
  <%= f.datetime_field(:updated_at, :value => "1984-01-12") %><br>
  <!-- <input created_at="2014-06-01" id="post_updated_at" name="post[updated_at]" type="datetime"> -->

  <%= f.label :email %><br>
  <%= email_field(@user, :email, :value => "Enter email here...") %><br>
  <!-- <input id="_email" name="[email]" type="email"> -->

  <%= f.label :fields_for %> --- Work in Progress ---<br>
  <%= fields_for :name, @post.name do |name_fields| %>
  Admin?  : <%= name_fields.check_box :admin %><br>
  <!-- <input id="name_admin" name="name[admin]" type="checkbox" value="1"> -->
  <%= name_fields.submit %>
  <% end %>

  <%= f.label :file_field %><br>
  <%= f.file_field(:file, :multiple => "true") %>
  <!-- <input id="post_file" name="post[file]" type="file"> -->

  <%= f.label :forms_for %> --- Work in Progress ---<br>
  <%= fields_for :name, @post.name do |name_fields| %>

  <%= f.label :month %><br>
  <%= f.month_field(:created_at, :value => "1984-01") %><br>
  <!-- <input created_at="2014-06-30" id="post_created_at" name="post[created_at]" type="month"> -->

  <%= f.label :number_field %><br>
  <%= f.number_field(:content, :value => 14) %><br>
  <!-- <input id="post_content" name="post[content]" type="number"> -->
  
  <%= f.label :password %><br>
  <%= password_field(@user, :password) %><br>
  <!-- <input id="_password" name="[password]" type="password"> -->

  <%= f.label :phone %><br><!-- telephone_field works too -->
  <%= phone_field(@user, :number) %><br> 
  <!-- <input id="_number" name="[number]" type="tel"> -->

  <%= f.label :radio_button %><br>
  <%= f.radio_button(:tags, "rant") %><br>
  <!-- <input id="post_tags_rant" name="post[tags]" type="radio"> -->

  <%= f.label :range %><br>
  <%= f.range_field(:updated_at)%><br>

  <%= f.label :search, "Search For..." %><br>
  <%= search_field(@user, :name, :onsearch => true) %><br>
  <!-- <input id="_name" name="[name]" onsearch="true" type="search"> -->

  <%= f.label :text_area, "This is a large text area!" %><br>
  <%= f.text_area(:content, cols: 50, rows: 10)%><br>
  <!-- <textarea cols="50" id="post_content" name="post[content]" rows="10"></textarea> -->

  <%= f.label :text_field %><br>
  <%= text_field(@post, :content, size: 20, :placeholder => “Add task” ) %><br>

  <%= f.label :time_field %><br>
  <%= time_field("task", "started_at") %><br>
  <!-- <input id="task_started_at" name="task[started_at]" type="time"> -->
  
  <%= f.label :url %><br> <!-- enforces url address -->
  <%= url_field(@user, "www.google.come") %><br>

  <%= f.label :week %><br>
  <%= week_field(@user, :created_at, :value => "1984-W19" ) %>
  <!-- <input id="_created_at" name="[created_at]" type="week" value="1984-W19"> -->
<% end %>

{% endhighlight %}

### Partials

We also have partials, which are reusable templates used as views for your app. Any time you find yourself repeatedly building the same view, turn it into a partial and keep your code DRY. They're great for headers, footers, navbars, and many others.

Files are denoted with an underscore (e.g. `_index.html.erb`). These views are important and should not be deleted without serious consideration!

### Render

And when you're ready to display your partials, simply throw in a render and you're good to go.

`<%= render 'form' %>`

And that's a quick and dirty jump into forms.