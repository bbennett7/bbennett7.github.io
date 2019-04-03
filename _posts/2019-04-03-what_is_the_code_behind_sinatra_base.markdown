---
layout: post
title:      "What is the code behind Sinatra::Base?"
date:       2019-04-03 16:53:37 +0000
permalink:  what_is_the_code_behind_sinatra_base
---


I learned recently, after studying the basics of Ruby and building Ruby methods, that using the Active Record Gem and simply inheriting Sinatra::Base takes care of a lot of this work for us. So I started to wonder - what is actually happening when I write this line of code?

We already know that Sinatra is built on ActiveRecord, which is built on Rack which is just Ruby code, and that on top of all of this, Rails is built on Sinatra. In short, each of these allows us to inherit methods that the gems have defines for us, so that we don't have to reinvent the wheel each time. But still I was curious about what this code actually looks like. 

I navigated to GitHub.com, where I found the base.rb file for Sinatra, which contains much more than just a Base class. Sinatra is a module, which contains a class of Request inheriting from Rack::Request and a handful of methods.

Sinatra then gives us private classes and more methods, starting with the AcceptEntry class, then the Response class which inherites from Rack::Response, ExtendedRack which inherits from Struct.new(:app), CommonLogger class which inherits from Rack::CommonLogger, and Stream, all of which have a number of methods defined within them (too many to list out here).

We then have a Templates Module, followed by the actual Base class.

The Base class includes Rack::Utils, Helpers, and Templates. It has attribute accssors of :app, :env, :request, :response, and :params, as well as an attribute reader of :template_cache, and then, of course, methods. Looking through the code here is helpful because we can see how each of the methods is actually written - what it is actually doing when we call it - and also has notes about its purpose. Below is a simple breakdown of the public methods and what they do, per the Base class code and notes:

* initialize(app = nil) - Your basic initialize method, accepting an argument of an app and defaulting to nil if one is not given. Initialize here also accepts a block if given.
* call(env) and call!(env) - Rack call interface.
* settings and self.settings - Allows access to settings defined with Base.set
* options - Gives a warning that the options method is deprecated and will be removed, then calls the settings method(above).
* halt(response) - Will exit the current block and halt any further processing, then returns the argument of response.
* pass(&block) - Passes control to the next matching route if available. If not available, will return a 404 response.
* forward - forwards request to the downstream app.

There are private methods, other classes, and other methods in this base.rb file - more than can be  touched on in one blog post. For those of you who are interested in a deep dive, you can find the actual code for Sinatra::Base inside of the base.rb file [here](https://github.com/sinatra/sinatra/blob/master/lib/sinatra/base.rb). 

