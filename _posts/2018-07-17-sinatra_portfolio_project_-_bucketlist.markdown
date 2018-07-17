---
layout: post
title:      "Sinatra Portfolio Project - BucketList "
date:       2018-07-17 22:53:37 +0000
permalink:  sinatra_portfolio_project_-_bucketlist
---


For my Sinatra Portfolio Project, I created a BucketList web app.  The idea is that app users can create buckets to keep track of ideas of things they would like to do.   Though you may put all these ideas, or goals, in one bucket, the app lets you create multiple buckets.   For example, you may have a bucket related to being a parent and another bucket for yourself.   Buckets are private – only the user who created them can view or modify.

A bucket has one or more goals.  Besides a name and description, each goal has optional links to additional information or an image.  And a goal can be marked as completed.

To inspire a user to think about goals, there is a database of ideas.   A user can browse these ideas based on categories (ex. Outdoors, Art, Sports) and create a goal from an idea.  When a goal is created from an idea, the user gets a copy of that idea that they can personalize.

So what did I learn during this project?   

A lot of the BucketList functionality is very similar to what we covered in the various Sinatra and ActiveRecord labs (example: users and sessions, has many – belongs to relationships).  For these areas, the project was good practice in bringing together ideas.   

One of the more interesting challenges was to come up with a reasonable user experience and then apply what we learned about Sinatra and RESTful routes.  In the labs, it seemed that we did it the opposite – we always sort of knew the routes and then we just adjusted the user interface.   In the BuckeList, I opted for a “dashboard” where a user could see all their buckets and goals (in collapsible panels).   As a result, the page has multiple “Add Goal” buttons and each one needs the corresponding button incorporated in the route.  The standard RESTful route to show a “create goal” form is `GET /goals/new` but I had to also keep track of the bucket.  So I ended up with `GET /buckets/:bucket_id/goals/new`.     I think, or maybe hope, that is reasonably consistent with the REST conventions.

In my BucketList, I am now crossing off Build a Sinatra App.

