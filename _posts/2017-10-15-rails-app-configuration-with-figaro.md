---
layout: post
title: Rails app configuration with Figaro
---

If you’ve used email functionality in your rails application to send an email, You might have used the environment variables to protect username and password. 

Credentials like password and API keys need to be kept secret. Environment variables are a great way to protect private data. Figaro was written to make it easy to securely configure Rails applications.

I’ll show you how to use [Figaro](https://github.com/laserlemon/figaro){:target="_blank"} gem to simplify the configuration for your rails application. Let's get started.

## Install Figaro

First, add the gem figaro to your gemfile.
```ruby
gem 'figaro'
```

Now run bundle install in the terminal to install the gem.
```sh
$ bundle install
```

Now run bundle exec figaro install. This will generate a commented config/application.yml file and automatically adds it to your .gitignore file to tell git that we wish to exclude application.yml from git.
```sh
$ bundle exec figaro install
```

Add your own configuration to this application.yml file and you're done!

## Configure Figaro

Given the following configuration file, just add your secret information in this application.yml file like this:
```yml
# config/application.yml

gmail_username: "your-username"
gmail_password: "your-password"
```

Replace your-username and your-password with your actual secret. 

Now in your environment files you can input your secret information. Figaro will use the correct data depending on your rails environment. 
```ruby
# action mailer configuration for gmail

config.action_mailer.smtp_settings = { 
  :address => "smtp.gmail.com",
  :port => 587,
  :domain => "gmail.com",
  :user_name => ENV['gmail_username'],
  :password => ENV['gmail_password'],
  :authentication => :plain,
  :enable_starttls_auto => true
}
```

Now your information is secure. Often, local configuration values change depending on rails environment. In such cases, you can add environment-specific values to your configuration file.

> Rails 5.1 now include a way to encrypt your secrets file.

Rails now allows management of application secrets in a secure way. I will post more details in the coming weeks.

Thank you, and Happy coding :smile:!
