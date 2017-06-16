+++
date = "2012-02-01"
draft = false
title = "Routing a Wordpress Blog Inside a Rails App"

+++

This post describe how to host a subdomain route for a alien application inside a Ruby on Rails app. Wordpress is used here as an example but these instructions work with any outside url.

If you do have control over the web server you can use a url rewrite to accomplish this. See steps for doing this using [Apache](http://www.igvita.com/2007/07/04/integrating-wordpress-and-rails/) or [nginx](http://www.kalzumeus.com/2009/08/22/using-wordpress-and-rails-on-the-same-domain/).

However what about when you have no control over the web server layer (such as when hosting the Rails application on Heroku)? The answer is to use the Rails routing engine do the routing.

```ruby config/routes.rb
 match "/blog" => redirect("http://yourwordpressblog.com"), :as => :blog
```

This will match any '/blog' route and redirect to your chosen domain.
