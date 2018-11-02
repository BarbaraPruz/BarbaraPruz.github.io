---
layout: post
title:      "news4u – a Rails React/Redux App"
date:       2018-11-02 04:50:51 +0000
permalink:  news4u_a_rails_react_redux_app
---

![](https://drive.google.com/uc?id=1jabbvykSDHXZlf1wtghZrRe7VJ5YvthA)

So many news sites out there with different spins on top stories and different topic focuses! News4u is a little app that lets a user see news feeds from their preferred sources.

The app is powered by the newsapi.org APIs.  Currently, news4u just uses English language news sources which include everything from mainstream US media to established international networks and publications, like the BBC and the Times of India, to online sites like the Huffington Post.  Most of the sources provide general news but some specialize in areas such as sports, technology, and business.

In terms of the app architecture, 
* the back end is Rails and is responsible for persisting user information including preferences.   Right now, preferences are limited to selected news sources but could be expanded to include favorite topics, other languages, etc.
* the front end uses React with Redux and handles all requests to the newsapi.

As a learning experience, this project was great!   It has enough complexity that forced me to think about where functionality should be implemented.  And I had to research areas really not covered much in the curriculum like JWT and React Styled Components (to keep CSS manageable).   The more I learned, the more ideas I had about additional functionality and ways to present information to the user.   I’m looking forward to trying some of these out!

