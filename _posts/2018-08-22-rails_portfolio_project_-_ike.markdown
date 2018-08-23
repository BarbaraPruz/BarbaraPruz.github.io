---
layout: post
title:      "Rails Portfolio Project -  ‘ike"
date:       2018-08-22 21:16:19 -0400
permalink:  rails_portfolio_project_-_ike
---


‘ike is the Hawaiian word for knowledge.

For main goal for the Rails portfolio project is to build a content management app.   I decided on a general knowledge base app.   Part of the motivation came from actual experience – when I worked in product support, our team created a knowledgebase to share information both internally and with customers.  We were encouraged to use Sharepoint for the knowledgebase.  In the end, this was workable but not always ideal.   We found Sharepoint much better for sharing documents and files.  For sharing small articles/posts, it could be a little convoluted both on the publishing and consumer sides.

So ‘ike is my first attempt at trying to build an app that would have met the needs of that product support team.  As a first attempt, it is sort of like a Release 0 – just enough to see where the challenges can be and start to get ideas about where the app can go.

When starting a project, I like to think about the user functionality. Who are the users? What do they want to do?  And how will they do that?

There are 2 general types of ‘ike users – the knowledge experts that create the content and the general users who consume that content.  In a more advanced analysis, I might want to consider personas like the casual once a month general user vs. the user who is using ‘ike almost every day.  But for Release 0, I’ll keep it simple.  What would a general ‘ike user want to do?  Things that came to mind 

* Sorting and searching through articles – maybe by title or topic.
* Save an article that is useful (sort of like a bookmark)
* Be able to check what is new in the knowledgebase.

The knowledge experts are the administrators for the knowledgebase.  They want to be able to do the same things as the general user.  But also need to be able to create and maintain content.   It would be ideal for the knowledge experts to get feedback on what articles customers find useful, and also, at times, to steer customers to content.

Based on this, I started to see the application models and relationships.  For example, Topics have many Articles and an Article belongs to a Topic.   And Users have many Articles through Bookmarks.

And the functionality started to identify routes :  Users need to login and logout, and of course, there will need to be CRUD for the Users.   Admin Users will need to be able to maintain (create, edit, delete) Articles and Topics.   All Users will need to be able to create and delete their Bookmarks.  Users will need to be able to “like” an Article.

With these ideas taking form, I started coding and filling in the additional details.  Check it out at [https://github.com/BarbaraPruz/ike](http://)

