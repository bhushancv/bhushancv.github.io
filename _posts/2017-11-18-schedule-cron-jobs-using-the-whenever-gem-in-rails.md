---
layout: post
title: Schedule Cron Jobs Using the Whenever Gem in Rails
---

Sometimes, we have to schedule a task to run periodically in our app. We can perform this by using the built-in cron. Cron is a piece of software written for unix system, which provides a command, called crontab, that allows users to create scheduled tasks.

You can edit your own crontab file using the crontab command.
```sh
$ crontab -e
```

Suppose you want to perform some task every day at 12:00 AM. Add the following line to the crontab file:
```sh
0 0 * * *  /usr/bin/somedirectory/somecommand
```

Cron uses above format to figure out the schedule for executing the job. To understand the cron syntax, here is the information for each field
```sh
* * * * * Command to be executed
| | | | | 
| | | | +---- Day of the Week   (range: 0-6, Sunday=0)
| | | +------ Month of the Year (range: 1-12)
| | +-------- Day of the Month  (range: 1-31)
| +---------- Hour              (range: 0-23)
+------------ Minute            (range: 0-59)
```

This can be done manually by hand in the crontab on the server, but the syntax is little complicated. 

The [Whenever](https://github.com/javan/whenever){:target="_blank"} gem is a wonderful gem that provides a clear syntax for writing and deploying cron jobs. We will see how to use this gem to schedule your tasks. Let’s get started.

Install the whenever gem by adding the most recent version of the Whenever gem to the gemfile.
```ruby
gem 'whenever', '~> 0.10.0', :require => false
```

Here :require => false means that the gem will be installed, but will not be loaded into a process unless you explicitly call require "whenever".

Now run bundle install in the terminal to install the gem.
```sh
$ bundle install
```

Now integrate Whenever into your project, for this go to the project directory and run the wheneverize command to create a schedule file
```sh
$ wheneverize .
```

This will create a config/schedule.rb file for us where we will write our tasks. This is one of the tasks I added to my schedule.rb file which will run everyday at 12AM.
```ruby
# config/schedule.rb
every 1.day, :at => '12:00 am' do
  rake "app_server:task"
end
```

After adding tasks into schedule.rb file run the whenever command. This will output a preview of the generated schedules in the actual cron format.
```sh
$ whenever
```

This will just show schedule.rb file converted to cron syntax. It does not read or write crontab file. We need to update crontab in order to execute tasks.
```sh
$ whenever --update-crontab
```

After running this, you should see:

<div class="message">
[write] crontab file updated
</div>

If you want to check that Whenever wrote your tasks correctly on the crontab, you can list installed cron jobs using crontab -l command.
```sh
$ crontab -l
```

In this way, we can create cron jobs using the whenever gem in rails and the  advantage of using the whenever gem is that you don’t have to remember the crontab syntax.

Thanks for reading, Hope that helped :smile:!
