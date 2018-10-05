---
layout: post
title:      "Rails - JavaScript Project - Using a JSON  Backend "
date:       2018-10-05 01:35:15 -0400
permalink:  rails_-_javascript_project_-_using_a_json_backend
---


For this project, I started with a general knowledgebase Rails app, ‘ike.   In case you are wondering, ‘ike is the Hawaiian word for knowledge.  Besides the app managing knowledge, I’m hoping this project extends my knowledge in meaningful ways.

One project requirement is to render an index page using Javascript with an Active Model Serialization JSON Backend.  The ‘ike navigation menu has an option for showing an articles index and that seemed ideal for the requirement.   In implementing this requiirement, there were2 principal changes (and a several  minor changes):

*** *How to render the initial index page from JSON?***

This is accomplished through 2 Rails routes.  The navigation menu links to the index route which renders an index page with a blank articles table.  In the index page’s Javascript document ready(), I call jquery $get() to the “index data” route.  This route returns the actual article index data, as JSON, which is then rendered by the Javascript using a Handlebars template.   Though this sounds complicated, the code is minimal and simple (take my word for it!).  
The index has no need for the article content and so on the Rails side, I customized the Articles serializer to just provide the data needed.  For a large knowledgebase, this dramatically reduces the amount of data returned by the $get.  

*** *How to handle sort?***

The sort field (topic, title, last update, etc.) is provided through a small form.   In the page’s Javascript, I implemented a handler for the sort form submit.  Similar to the initial index display, this handler uses the “index data” route with the sort field.  In the earlier version of the app, the sort function caused a complete page redraw.  With the JSON backend, only the articles table information is updated.  A nice improvement in the user experience!

In testing, I noticed an unexpected side effect – on any page load for the app, the index page’s javascript document ready() executes.  Since this code has an ajax call, it created unnecessary message traffic.   One possible solution is to take the index page’s Javascript out of the asset pipeline and just directly add it to the index html page.   I didn’t really like this approach – for maintaining the app, it just seems nicer to keep the Javascript separate.   Instead, I opted for having the document ready() verify the page loaded before calling $get().   This required modifying the application layout - it now adds controller_name and action_name classes to the body.  Any Javascript can check for these values and adjust its behavior accordingly.

So what did I learn?   There are lots of small headaches moving to a JSON backend.  But there are definite benefits in a smoother user experience.   No more of that reloading complete pages just to update one section.  When designing an app, this opens up the possibilities for providing functionality in interesting ways to the user. 

