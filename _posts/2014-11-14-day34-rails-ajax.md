--- 
layout:     post
title:      "FS // Day 34 | Rails - Ajax"
date:       2014-11-14 10:00:00
categories: flatironschool rails javascript
tags:       javascript, ruby, rails, javascript, ajax
---

Whenever you type in a web address and hit 'enter', you initiate an HTTP request which typically flows like this:

* browser makes a request to server
* server parses the response (fetches page)
* server fetches the assets (js, stylesheets, images)
* then assembles and shows page 

Asynchronous JavaScript and XML (Ajax) allows an application to do this for a specific part of itself without having to reload the entire page.

### Unobtrusive JS

UJS is the technique of attaching JavaScript to the DOM. Its major benefits include:

   * not mixing JS into the HTML
   * separation of concerns; makes future changes easy
   * able to serve entire JS bundle on every page where first load is downloaded and then cached on every other page.

### Built-in Helpers

Rails comes with a bunch of helpers for making Ajax magick happen. Here's the list:

* `form_for`
* `form_tag`
* `button_to`

Say you wanted a form that could create a new list. You could use `form_for` helper like this:

{% highlight erb %}
<%= form_for(@list, remote: true) do |f| %>
  ...
<% end %>
{% endhighlight %}

which will generate as HTML:

{% highlight html %}
<form accept-charset="UTF-8" action="/lists" class="new_list" data-remote="true" id="new_list" method="post">
  ...
</form>
{% endhighlight %}

note: `data-remote=true` means the form will be submitted via Ajax rather than browser’s normal submit mechanism.

Without `remote: true` in your Ruby code, you would need the following JavaScript to handle the submit event:

{% highlight js %}
$("form").on("submit", function(e) {
    e.preventDefault();

    var form_method = $(this).attr("method");
    var form_action = $(this).attr("action");
    
    $.ajax(form_action, {
      type: form_method,
      data: $(this).serialize(),
      dataType: "script"
    })
  });
{% endhighlight %}

But because this is Rails, you don't need to do any of that!

Similarly, `form_tag` and `button_to` offer similar functionality:

{% highlight erb %}
<%=form_tag('/articles', remote: true) do %>
  ...
<%end%>

<%=button_to "An article", @article, remote:true %>
{% endhighlight %}

which will generate these two separate HTML forms:

{% highlight html %}
<!-- this is using form_tag -->
<form accept-charset="UTF-8" action="/articles" data-remote="true" method="post">
  ...
</form>

<!-- this is using button_to -->
<form action="/articles/1" class="button_to" data-remote="true" method="post">
  <div><input type="submit" value="An article"></div>
</form>
{% endhighlight %}

note: `button_to` generates an entire form with a single button in it. 

### Server-side concerns

Here a simple example of some interaction between Ajax and Rails:

Within the index action of a controller:

{% highlight ruby %}
class UsersController < ApplicationController
  def index
    @users = User.all
    @user = User.new
  end
  # ...
{% endhighlight %}

Inside of the index view:

{% highlight erb %}
<b>Users</b>

<ul id="users">
  <%= render @users %>
</ul>

<br>
 
<%=form_for(@user, remote: true) do |f| %>
  <%= f.label: name %><br>
  <%= f.text_field: name %>
  <%= f.submit %>
<%end%>
{% endhighlight %}
        
and lastly, within the _user partial:

{% highlight coffee %}
<li><%= user.name %></li>
{% endhighlight %}

Here the form calls the `#create` action on UsersController. Because remote = true, the request will be posted to the UsersController as an ajax request looking for JS. In order to serve the request, the create action for controller has to look like the following:

{% highlight ruby %}
# app/controllers/users_controller.rb
# ......
def create
  @user = User.new(params[:user])
 
  respond_to do |format|
    if @user.save
      format.html { redirect_to @user, notice:'User was successfully created.'}
      format.js   { }
      format.json { render json: @user, status: :created, location: @user}
    else
      format.html { render action: "new"}
    end
  end
end
{% endhighlight %}

**notice format.js**: the empty block allows the controller to respond to ajax request. Here we can use a corresponding create.js.erb view to generate JS code that will be executed on the client side:

`$("<%= escape_javascript(render @user) %>").appendTo("#users");`

or more simply, you could write the JS shorthand: 

`$("<%= j render @user %>").appendTo("#users");`

### Turbolinks

Rails also comes equipped with Turbolinks, a gem that:

* uses ajax to speed up page rendering in most apps
* attaches click handler to all <a> tags
* if PushState supported, turbolinks makes ajax request for page, parses the response, and replaces entire <body> of page with response body. Then changes URL to correct one
* to enable: put `//= require turbolinks` in coffesescript manifest `/app/assets/js/app.js`
* to disable: add `data-no-turbolink` to any a tag like so: 

`<a href="..." data-no-turbolink>No turbolinks here</a>.`

In my limited experience so far, I've found that Turbolinks adds more headache than help, especially when trying to debug ajax issues.







