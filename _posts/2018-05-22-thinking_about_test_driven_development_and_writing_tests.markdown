---
layout: post
title:      "Thinking about Test Driven Development and Writing Tests"
date:       2018-05-22 23:53:17 +0000
permalink:  thinking_about_test_driven_development_and_writing_tests
---


Anyone any where near the Learn environment knows that it heavily uses test driven development (through rspec) to verify progress. This is great - everyone can efficiently work through the labs independently and get the same feedback.   

Students aren't writing their own tests.  Though we use test driven development, we really aren't learning how to write
tests.  The Learn test specs are a little unique in that they are often not just verifying the code works but that it uses a feature being currently covered in the curriculum.  So this got me thinking - what would make a good test?

What I really value about test driven development is that after that 1st delivery, the programmer has tests that can be 
very easily utilized for regression testing after code is later enhanced, improved or just re-factored.  The tests also let a programmer pass on some intents to the next developer maintaining the code. In "a past life", I designed a console (display+keyboard) driver for a point of sale terminal.  I took a lot of care to use encapsulation to keep the tricky parts of the logic hidden. For example, the Cursor object was the only code that knew how to position and draw a cursor. I moved on to different projects and in the meantime, the driver was enhanced to support "right to left" languages like Hebrew or Arabic.  Later, I was investigating a problem and had to  check the console driver code.   I found that the "right to left" implementation bypassed the Cursor object and just directly drew a cursor whenever and wherever. All I can say is that I was glad to not be the next person to maintain that code!

When creating tests, its obvious that you want to verify the interface (ex. class methods) and to include an appropriate
level of exception testing (bad parameters, etc.).  But sometimes, there may be additional tests to consider where the 
purpose is to verify key design elements.   Applying this to Ruby, it might be something like verifying a model that inherits from ActiveRecord doesn't accidentally override the ActiveRecord attribute accessors.  

There is a balancing act in all of this - the test specs need to be complete but also maintainable.  In the end, the test specs are an all round good investment not just to help the initial developer but for the lifetime of the code.
