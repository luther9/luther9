---
layout: post
title: Blocipedia
short-description: A wiki.
---

# Summary

A web site where users can create and edit wikis.

# Devise

We use Devise to sign up and authenticate users. This is very different from
authorizing manually in the controller.

# Flash

Flash messages are typically set in the controller using the `flash` hash. They
are meant to show the user a response to their actions. We show these messages
in `app/views/layouts/application.html.erb`.

# Faker

Faker was very useful for writing the seed file and for unit tests. I had
previously written a seed file so I could observe my previous work on the web
site, but Faker allowed me standardize the code a bit better.

For the User class, Faker had obvious functions I could use for each of the
fields. For the Wiki class, however, I had to use my own judgement. I wrote a
FakeWiki module so my choices would be consistent throughout the app.

```ruby
# A library with functions parallel to Wiki attributes. They return random
# values for those attributes.
module FakeWiki
  def self.title
    Faker::Company.catch_phrase
  end

  def self.body
    Faker::Hipster.paragraph
  end
end
```

At first I named the FakeWiki file random_data.rb. After some error messages, I
found out that the file name needs to be the same as the module or class name
(but with lowercase and underscores). After I corrected the file name, it was
automatically `require`'d throughout the app.
