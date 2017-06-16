+++
date = "2012-03-09"
draft = false
title = "Using Pry With Rails"

+++


[Pry](http://pry.github.com/) is a IRB replacement with some very nice additional features. I'll link to additional resources at the end of this post.

Some of the additional features pry offers us include:

* Native syntax highlighting
* Source and document browsing
* Very flexible plugin architecture

##Installation

You can install and run pry with:

```
$ gem install pry
$ pry
```

They are a few ways to integrate pry with Rails but the one I like it the most came from [@fnando](http://twitter.com/fnando) and originally from [Luca Pette](http://lucapette.com/pry/pry-everywhere/). Instead of patching of Rails initializer file, as described on the [Pry Wiki](https://github.com/pry/pry/wiki/Setting-up-Rails-or-Heroku-to-use-Pry), you can use the following method:

On IRB initialization file load Pry instead:

```
begin
  require 'pry'
  Pry.start
exit
  rescue LoadError => e
  warn "=> Unable to load pry"
end

```
This will load try to load Pry and if failed will print a message to stdout. The exit command after Pry's invocation is to avoid going back to IRB after the Pry session has finished.

The other part of the configuration is done on .pryrc

File: ~/.pryrc
```
if defined?(Rails)
  begin
    require "rails/console/app"
    require "rails/console/helpers"
  rescue LoadError => e
    require "console_app"
    require "console_with_helpers"
  end
end
```

This will allow you to continue using rails console but using pry instead of irb. I also like to use awesome_print so I added this to my config file:

File: ~/.pryrc

``` ruby
begin
  require "awesome_print"
  Pry.config.print = proc {|output, value| Pry::Helpers::BaseHelpers.stagger_output("=> #{value.ai}", output)}
rescue LoadError => err
   warn "=> Unable to load awesome_print"
end
```

This will try to load awesome_print gem and failing to do that will print a message to stdout.

For more information on Pry see:

* [Pry's website](http://pry.github.com/)
* [Pry Railscast](http://railscasts.com/episodes/280-pry-with-rails)
* [My irbrc](https://github.com/filipeamoreira/dot-files/blob/master/_irbrc)
* [My pryrc](https://github.com/filipeamoreira/dot-files/blob/master/_pryrc)
