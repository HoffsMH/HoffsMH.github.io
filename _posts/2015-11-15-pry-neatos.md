---
layout: post
title:  "Pry neato's"
subtitle: "Fun with pry!"
date:   2015-08-19 23:56:45
categories: [tool]
---

This post is an adaptation of a lightning talk I gave. Its basically just some of the tools
and tricks I've learned about while using pry and ruby. Hopefully I will come back to it later and make it more like a blog and less like a talk outline. But for now just posting this for some friends!.

There is some accompanying demo code available at [github](https://github.com/HoffsMH/pry-lightning-talk)

___


# Basic neato's

Some random things I've found useful that can be used with pry out of the box.
* ``` whereami ``` to remember where you are in your code

* ```.<command> ``` executes terminal commands
  * ``` .ls ```
  * ``` .clear ```
  * ``` .git diff ```
  * ``` .git status ```
  * and yes we can get crazy ```.ruby <some-other-file> ```


and assuming your pry doesn't completely crash when an exception occurs because you are using pry-rescue.
* ``` wtf ``` and ``` wtf? ``` to display stack traces for an exception

* ``` cat -ex ``` to bring you to the line in your code where the exception occurs

* We can edit a file while in pry then continue to run through it with ```edit <filename> ```
  * but first we should probably set out editor with  
  ``` Pry.config.editor = 'atom'/'vim'/'whathaveyou' ```

  * or just include that line in ``` .pryrc ``` in our home directory


## Other Neato's
Cool ways of using pry.
* ``` binding.pry ``` is just ruby.

  So we can put a condition on whether or not it runs for when we know when something is going wrong but don't want to type exit 231 times.

  ```ruby
  [*1..1000].each do |element|
    if element == 232
      binding.pry
    end
  end
  ```

* We can also get pry to be the default debugger in rails by including ``` pry-rails``` instead of just ```pry``` in your gemfile


  ```ruby

  #gemfile
  group :development, :test do
    gem 'pry-rails'
  end

  ```

  ```bundle``` then type ```rails c ``` and you're in pry and not irb!


## Things to install and try
* ## [Pry-toys](https://github.com/ariabov/pry-toys)
  * For when you need to test something for yourself really quick. Really usefull for understanding enumerables.

    ```bash
     gem install pry-toys
     ```

   * #### Try

     ```ruby
    Hash.toy(300) # creates a toy has
    Array.toy(3, Time) # creates a toy array of Time objects
     ```

* ## [Pry-byebug](https://github.com/deivid-rodriguez/pry-byebug)
 * for stepping through code.
 Serves as a fine comb to step through and understand code one line at a time.
 * was originally a fork of [pry-debugger](https://github.com/nixme/pry-debugger) which [doesn't work past Ruby version 2.x](http://stackoverflow.com/questions/24395453/gem-install-debugger-error)
   ```bash
    gem install pry-byebug
    ```

 * #### Try

    ```ruby
   step # Moves through code line by line
   continue # completes rest of code
    ```
* ## [Pry-rescue](https://github.com/ConradIrwin/pry-rescue)
  * from the author of this gem

    "start a pry session when something goes wrong"

    this is actually a two parter

    ```bash
    gem install pry-rescue
    gem install pry-stack_explorer
    ```
    both must be installed to work properly

  * #### Try

    ```bash
    rescue <problematic ruby file>
    ```

    #### and yes it can be used with rails

    ```bash
    rescue rails s
    ```
