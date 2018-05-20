---
layout: post
title: How to prevent the browser page caching in Rails
---

If you have configured devise for an authentication solution in rails applications. 
You will find a browser back button issue after logout.

When any user sign into any web application, we store some value in the session. The session proceeds with the user presence until logout. After logout we clear/kill the session and divert to a specific page. In that state, the user is out of the site and should not be able to access the page which needs authentication.

However, the issue is currently, from this divert page if client taps the back button of browser, it again goes to the previous visited page although the page is already logged out. 

The primary cause is the browser’s cache. This is because while user logs out the session, the session is relinquished in the server side. So, if you click the back button of the browser, the previous page will not postback, the client side will open from cache. It will only function if back page is refreshed, because in that case the page will become postback.

The problem has many solutions, but each and every solution has some limitations. One way to fix it is to remove the caching from the logged in pages for preventing this issue.

You will have to set the headers of your page to prevent caching. You can set it in the application controller.
```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base

  before_action :prevent_caching

  private

  def prevent_caching
    response.headers["Cache-Control"] = "no-cache, no-store"
    response.headers["Pragma"] = "no-cache"
    response.headers["Expires"] = "Fri, 01 Jan 1990 00:00:00 GMT"
  end
end
```

> before_filter has been deprecated in Rails 5.0 and removed in Rails 5.1. before_action is just a new syntax for before_filter.

In this way, we can solve the browser back button issue after logout and prevent browsers from caching a page in rails.
