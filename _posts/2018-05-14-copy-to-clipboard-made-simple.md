---
layout: post
title: Copy to Clipboard Made Simple&#58; How to Copy to a User’s Clipboard in Rails
---

Web technology is changing with alarming frequency these days.

Nowadays some websites need a feature to copy some text, such as a paragraph, code snippet, or a URL to clipboard, without selecting the text. We can easily do this using Javascript.

You can use browser APIs for copying to the clipboard, but it’s not an easy way of copying text to the clipboard. Copying text to the clipboard should be hassle free. It shouldn't require dozens of steps to configure or hundreds of KBs to load.

The [ZeroClipboard](https://github.com/zeroclipboard/zeroclipboard){:target="_blank"} library provides an easiest way to do this using an invisible Adobe Flash movie and a JavaScript interface. 

I had used ZeroClipboard in some of our projects, but I'm more concerned about the users that don't have Flash and this functionality is going to be broken for them.

So one of the best ways to do that is by using the [clipboard.js](https://clipboardjs.com/){:target="_blank"} because it does not rely on Flash. It’s a modern approach to copy text to clipboard without Flash.

It’s a modern alternative to ZeroClipboard (which is Flash based) to copy text to clipboard.

In Ruby on Rails you can use clipboard.js by downloading and adding the javascript file to the asset pipeline, or you can even use the [clipboard-rails](https://github.com/sadiqmmm/clipboard-rails){:target="_blank"} gem.

> clipboard-rails gem is the integration of clipboard.js javascript library for your Rails 4 and Rails 5 applications.

Following are the steps to use clipboard.js (without using gem) in rails: 

1. Download the clipboard.js file.
2. Add a clipboard.js file to the app/assets/javascripts folder.
3. Now you need to edit your application.js file and add the following line:
```javascript
//= require clipboard
```

4. Create a template file like index.html.erb, and add this sample code to your file.
```erb
<!-- Target -->
<%= text_field_tag :weburl, "https://bhushanjadhav.info/" %>
<!-- Trigger -->
<%= button_tag "Copy", :type => "button", :id => "clipboard-btn", :data => {:clipboard_action => "copy", :clipboard_target => "#weburl"} %>
```

5. Create a javascript file, and add this sample code to your file.
```javascript
var btn = document.getElementById('clipboard-btn');
var clipboard = new ClipboardJS(btn);  
// Success
clipboard.on('success', function(e) {
 console.log(e);
});
// Error
clipboard.on('error', function(e) {
 console.log(e);
});
```

That's it! You should now be able to copy text to your clipboard by clicking on the button.

Thanks for reading, Hope that helped :smile:!
