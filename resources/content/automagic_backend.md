Automatic backend
-----------------
August 2013

I generally dislike writing backends for one-off projects and prefer to rely on
things like Django's built-in administration interface. It works fine, even in
production, but it isn't the prettiest of the bunch. That's OK. That's not the
main focus, and it shouldn't be.

But say I'm not using Django. Maybe I'm using nodejs. Maybe, I'm a Flask-man. I
still don't want to roll my own backend.

So, I have an idea for an automatic backend that you point to an empty database
and a directoy that contains some files.

Given the HTML-structure I should be able to generate a passable database model
and from that, generate relevant controls for adding content. Quick 'n' dirty
style web-development, *aha*, just the way, *aha*, I like it.

Most data that we need is contained in the templates, but some conventions are
needed for our backend to be able to pick up various models, and to start we 
would have to restrict ourselves to a template format, but keep it generic
enough so we can plug in new template formats.

A simple example would be:

    {% for user in users %}
      {{ user.id }}, {{user.name}}
      <ul>
        {% for post in users.posts %}
          <li>{{post.title}}<br/>{{post.description}}</li>
        {% endfor %}
      </ul>
    {% endfor %}

From this we can deduce that there are many users, so we can build a table 
called "users" to contain those. We can then deduce that there are posts
related to a user, so we can establish that a model is needed for that as well.

Thinking about it, it is probably wise to try to generate the models from this 
information, and then try to generate a database model from those models, so we 
go deeper and deeper. This also means that our tools are neatly divided, and if 
we want to write our models instead, we are still able to generate a backend
from those.

/v.
