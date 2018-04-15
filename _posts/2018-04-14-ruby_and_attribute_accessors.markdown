---
layout: post
title:      "Ruby and Attribute Accessors"
date:       2018-04-15 02:02:42 +0000
permalink:  ruby_and_attribute_accessors
---

Ruby’s attribute accessor macro’s provide a simple succinct way to define getter/setter methods for instance variables.   Anyone coming from some other programming languages knows the tediousness of creating getter/setters and the inevitable typo’s to be found and corrected.   So I’ll have to call this one of Ruby’s contributions to improving the quality of life for programmers. 

There are 3 variations on these macros:
```
attr_accessor   :my_variable    # creates getter method my_variable and setter method my_variable=
attr_reader   :my_variable          # creates getter method my_variable 
attr_writer   :my_variable            # creates setter method my_instance_variable=
```

Besides saving typing, these macros also can provide a little “structure” to you code – for the next programmer reading your code, it’s easy to see where you are using the default accessor methods.    

One concern about these macros is related to the writer methods.  Ruby makes it so easy, the tendency is to just provide the default writer method.  But your class logic relies on the integrity of its data.  If an instance variable value need to be within a certain range or type, the default writer can cause problems.  Imagine a room thermostat being set to 425 (the user got confused and thought they were roasting vegetables).  Or maybe the thermostat is set to “comfortably cool”.   For example

```
class Thermostat
    attr_accessor :selected_temperature
    def initialize
      @selected_temperature = 72
    end
  end
  
  t = Thermostat.new
  t.selected_temperature  
   => 72
  t.selected_temperature="I like it hot!"
   => "I like it hot!"
  t.selected_temperature
   => "I like it hot!"
```
Good implementations should catch these issues at the time assignment is attempted.  

All in all, attribute accessors are great.  But I’ll need to remember to consider if default writer is a bad choice.   I guess that is part of writing good test specs!


