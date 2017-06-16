+++
date = "2012-01-24"
draft = false
title = "Full Text Search With MongoDB"

+++

Recently I had to implement full text search on a Ruby on Rails application.  Based on the app's needs the best way to do it was building a helper array with the keywords needed and make the search using those keywords.

To illustrate this I've implemented stock tickers search using the awesome [rstat.us](http://rstat.us/) project. Have a look at my [Github fork.](https://github.com/filipeamoreira/rstat.us)

File: `update.rb`

{{<highlight ruby>}}
class Update
...
    # Adds stocks array mentions
    key: stocks, Array, :default => []

  # Parses update text and build stocks array for simpler search
  def parse_symbols
    stocks = []
    self.text.split(' ').each do |update|
      stocks << update if update[0] == '$'
    end
    return stocks
  end
end
{{</highlight>}}
and then the controller:

File: `updates_controller.rb`

{{<highlight ruby>}}
class UpdatesController < ApplicationController
...
    def create
      ...
      u = Update.new(:text => params[:text],
          :referral_id => params[:referral_id],
          :author => current_user.author,
          :twitter => do_tweet)

      u.stocks = u.parse_symbols
      ...
    end
end
{{</highlight>}}

So it basically looks for words starting with $ and adds it to the stocks array. We can then search using

{{<highlight ruby>}}
Update.all(:conditions => {:stocks => '$goog'})
{{</highlight>}}


There are different solutions such as [mongoid_search](https://github.com/mauriciozaffari/mongoid_search) that could be used but for my needs this approach works the best.

MongoDB gives a lot of flexibility for the developer and speeds things up. Of course there are trade-offs to be made while using so YMMV.
