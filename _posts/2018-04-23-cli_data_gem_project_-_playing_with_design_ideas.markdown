---
layout: post
title:      "CLI Data Gem Project - Playing with Design Ideas"
date:       2018-04-23 21:02:43 -0400
permalink:  cli_data_gem_project_-_playing_with_design_ideas
---


The CLI Data Gem Project requires scraping an external web site and providing access to the data through a command line interface.   For my project, I chose the  Christian Science Monitor(CSM) news site -  [https://www.csmonitor.com/](http://).   This CLI gem presents a list of story titles.  If a story is selected, a story summary is displayed with URL to full article.   *Yes - this is a little lame!  Why use a CLI to get a URL and view story in browser?   Why not just browse the right page?   But anyway, we'll go with the project as a learning experience*.

In the curriculum, there have been several scraping labs that use similar designs.  In the Student Scraper lab, there are 3 classes - CLI, Student "data holder", and Scraper.  The interesting part is how the data gets populated.   Using similar class interfaces for my project, the interactions look like this:

![Original Design](https://drive.google.com/uc?id=15TUH8Se9yJJgUeiKlodoMewiP4T2LDCI)

This approach seems reasonable and originally, I was just going to copy it.   But then I thought it might be fun to play around. When checking design, it is always interesting to ask a few questions like are responsibilities encapsulated?   Is there duplication of code?    I also like to keep in mind that code often lives on much longer than planned.  It gets 
enhanced or evolves into a different app.  So I try to imagine potential enhancements or how the app code might be re-used in a related application.   

For example with the News CLI, if CSM provided an API, the gem should use that interface (better than scraping). Or what if the gem is expanded to also get news stories from other sites?   For these types of changes, will the class interfaces stand up? Is rewrite needed?   I don't want to actually code these dreamed up requirements - I just want to consider how they might look.   

Here is what jumps out:

- The CLI knows it is scraping and it knows it needs to scrape two different pages to get the information. This can be better encapsulated in the Scraper class.

- To support multiple sites, it makes sense to have a "news source" base class with a generic "get me today's 
stories" interface.   Child classes can implement whatever is needed to get the information from their specific site.

After a few iterations, here is the new design. The CLI just tells the Story class to create stories using a source (CSMScraper).   The Story class tells the Source to collect stories - each story collected includes all the attributes required by the gem.  

![Revised Design](https://drive.google.com/uc?id=1efLV9hVJpPK6ur409gXWSgkGDWzd3p0F)

Now to meet my dream requirements

- To use CSM Web API, the CLI just tells the Story class to use a different source (and of course a new class for the CSM Web API is  written)
- 
- Multiple news sources?   This is where adding the "News Source" class hierarchy makes sense.  The CLI can call the Story class multiple times with different specific sources.   In this situation, it probably makes sense to add a Story attribute "source".

There are many valid approaches to the same problem.  I think this tweaked design may be more robust without adding any real overhead to the gem.




