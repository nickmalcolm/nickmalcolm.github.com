---
title: "Making a Rails Health Check which doesn't hit the database"
excerpt_separator: <!--more-->
---

<div class="alert">
<strong>Note:</strong> This post was written for and originally published on the <a href="https://thisdata.com">ThisData</a> blog in 2016. Ages ago! I have reposted it here in case it's useful in the future.
</div>

In a production application you usually have many servers, and each of those servers get checked periodically to make sure they're still alive. If they are, then requests can be routed at them, for example by a load balancer. If a server doesn't respond to the healthcheck, then it is presumed to be dead or unhealthy, and requests are sent to the healthy servers instead. When your production environment uses automated scaling, servers can be killed and rebooted when they're unhealthy too.

<!--more-->

In a Rails app, a health check might look like this:

```ruby
class HealthcheckController < ApplicationController::Base
  def alive
    User.first
    render json: { ok: true , node: "I'm alive!"}
  end
end
```

When the healthcheck is called, it will hit the DB by checking for the first User record, and if that works, send a successful response. This is advantageous because if it can't talk to the database, then that server isn't going to be much use to your users. Most of the time that's true.

But if your database goes down, _all_ of your servers will go down too, because none of them can access the database. If you have autoscaling, all of your servers will continuously be torn down and set up.

You might think that all you have to do is remove the database call, and then your healthcheck will pass. Unfortunately this isn't true, because of Rails' default Middleware. Middleware are bits of code which a request is passed through before it hits your app proper. You can see [a list of Ruby on Rails' default Middleware stack here](http://guides.rubyonrails.org/configuring.html#configuring-middleware).

Have a go! Shut down your local database, and see what happens when you hit your healthcheck. For me on Postgres I get


PG::ConnectionBad
could not connect to server: Connection refused Is the server running locally and accepting connections on Unix domain socket "/tmp/.s.PGSQL.5432"?
 

Here's why. One of those pieces of Middleware is `ActiveRecord::QueryCache` ([view the source here](https://github.com/rails/rails/blob/160cc331796ebfbcd6da83e96f391ab5732832b6/activerecord/lib/active_record/query_cache.rb#L27-L29)). That middleware is executed on every request, before that request even makes it to the controller action. It connects to the database and enables a caching layer in ActiveRecord. So when a request comes in, and your database is down, this middleware will throw a big error. Since your healthcheck is way up further in the stack, in a controller action, it never gets a chance to run!

To get around this, you'll need to create your own middleware which comes before `ActiveRecord::QueryCache`.

_Side note: if you have a seperate marketing site which has its own seperate healthcheck, then it should hopefully stay up, and you might not need to create a healthcheck which doesn't hit the database._

## Implementing a Ruby on Rails middleware healthcheck

```ruby
class MiddlewareHealthcheck
  OK_RESPONSE = [ 200, { 'Content-Type' => 'text/plain' }, ["I'm alive!".freeze] ]

  def initialize(app)
    @app = app
  end

  def call(env)
    if env['PATH_INFO'.freeze] == '/healthcheck'.freeze
      return OK_RESPONSE
    else
      @app.call(env)
    end
  end
end
```

Save that in your app to `/app/middleware/middleware_healthcheck.rb`. In your `/config/application.rb` file, add the following line:

```
config.middleware.insert_after "Rails::Rack::Logger", "MiddlewareHealthcheck"
```
 
Now when your app starts Rails will add our new healthcheck middleware after initializing the logger, which also happens to be ahead of `QueryCache`. The middleware will "capture" any requests to `/healthcheck` and immediately return a 200 text response with _"I'm alive!"_ in the response body.  No more database calls!

In the code we've frozen some strings to reduce object allocation, which is handy for frequently called bits of code. I've called it `MiddlewareHealthcheck` because, well, it only checks that a request reaches the Middleware layer, and that's it! You should also add a comment to your `routes.rb` file, so that there's less chance for confusion.

So there we have it! A simple middleware for Ruby on Rails which intercepts healthcheck requests so that you don't have to hit the database. You could go ahead and add more Healthchecks which test for the availability of your other dependencies, to get a more complete picture of your system's status:

  - Is the App responding (example above)
  - Can the App talk to the database?
  - Can the app talk to your cache layer?
  - Does the homepage load? (a more traditional end-to-end healthcheck)