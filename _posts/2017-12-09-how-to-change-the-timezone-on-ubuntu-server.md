---
layout: post
title: How to change the timezone on Ubuntu Server
---

In one of my project, there was a requirement to schedule a cron job that will run a script every day at 12AM. So I followed the steps which I had mentioned in my previous post to schedule a cron job. 

Cron job was required to run in Australia/Sydney timezone. But the default timezone of the server was different. So I decided to change the timezone of the server.

Suppose you want to change the timezone of your server to Australia/Sydney timezone, then you can follow the steps below.

You can check your current timezone in ubuntu by simply running:
```sh
$ date
```

Now if you need to change the current time zone to Australia/Sydney or something else, then you will have to simply run:
```sh
$ sudo dpkg-reconfigure tzdata
```

You will be prompted with a list of timezones that you can select from. Just follow on screen instructions and change the timezone to Australia/Sydney or something else as per your requirement.

Now, as your cron job depends on timezone, you will have to restart the cron job after making your timezone change as it will not pick up the timezone change.
```sh
$ sudo service cron restart
```

In this way, you can change the timezone on ubuntu. Hope it will save your time.

Thank you, and Happy coding :smile:!
