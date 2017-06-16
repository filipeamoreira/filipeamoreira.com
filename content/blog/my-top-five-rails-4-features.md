+++
date = "2013-11-07"
draft = false
title = "My Top Five Rails 4 Features"

+++

[Rails 4](http://weblog.rubyonrails.org/2013/6/25/Rails-4-0-final/) was released last June and version [4.0.1](http://weblog.rubyonrails.org/2013/11/1/Rails-4-0-1-has-been-released/) at the beginning of this month. It should be noted that Rails 4 requires Ruby 1.9.3 with Ruby 2.0 being recommended.

Here I highlight my top five features:

## Strong Parameters

Rails Mass assignment feature is quite handy but can be really dangerous. Last year Github was [compromised by an attack based on it](http://www.infoq.com/news/2012/03/GitHub-Compromised). Rails 4 has a new way of dealing with mass assignment each basically pushes the responsibility out of the model and into the controller where it belongs.

The new approach was already available as a plugin called [strong_parameters](https://github.com/rails/strong_parameters) and dhh as a blog post [explaining it in detail](http://weblog.rubyonrails.org/2012/3/21/strong-parameters/).

## Live Streaming

Rails 4 brings Lives Streaming as a major new feature. To enable streaming we need to mixin the ```ruby ActionController::Live ``` to the controller class. One use case for this is to enable push notifications to the frontend without relying on plugins like [Juggernaut](http://juggernaut.rubyforge.org/) or outside services such as [Pusher](http://pusher.com/).

You can read more about this feature [here](http://www.sitepoint.com/streaming-with-rails-4/) and [here](http://blog.phusion.nl/2012/08/03/why-rails-4-live-streaming-is-a-big-deal/).

## Russian Doll caching

Russian Doll caching describes the technique of using nested fragment caching. The idea is that a page can best divided multiple sections, each one being a fragment. These cached fragments are used independently and can be reused when the content changes. Changes to inner fragments caused a chain reaction which expires all outer fragment caches. Rails 4 uses caches digests to avoid the pain of maintaining cache version numbers for individual templates.

You can read more about Russian Doll caching [here](http://37signals.com/svn/posts/3112-how-basecamp-next-got-to-be-so-damn-fast-without-using-much-client-side-ui)

## Asynchronous Action Mailer

A new Queue framework was added to Rails 4 and Action Mailer are configured by default to use this new Queue interface. The interface remains very similar to Rails 3 developers with the added benefit that changing backend providers is as easy as changing a single line of code:

```ruby
# production.rb
config.queue = ActiveSupport::Queue.new
# In this case to use Sidekiq as the Action Mailer backend
config.action_mailer.queue = Sidekiq::Client::Queue.new
```

You can read more about this feature [here](http://blog.remarkablelabs.com/2012/12/asynchronous-action-mailer-rails-4-countdown-to-2013)

## Other smaller enhancements

Rails 4 is now thread-safe by default. You can read about this change on this helpful [post](http://tenderlovemaking.com/2012/06/18/removing-config-threadsafe.html) by Aaron Patterson.

Another addition is Turbolinks which works similarly to pjax, fetching relevant content and updating the page to avoid a full reload. Read more about it [here](http://blog.remarkablelabs.com/2012/12/turbolinks-rails-4-countdown-to-2013)

There are many more features that I will not be able to cover here. You can read the [releases notes](http://edgeguides.rubyonrails.org/4_0_release_notes.html) to see the detailed changes.

Rails 4.0.1 brings some stability improvements to Rails 4. The complete set of changes are shown [here](http://weblog.rubyonrails.org/2013/11/1/Rails-4-0-1-has-been-released/)
