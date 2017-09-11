---
layout: post
title: Stuck on Jekyll Install
---

<h3>"ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory"</h3>

When setting up this portfolio, I ran into what seemed like an insurmountable snag while trying to [install the Jekyll Ruby Gem](https://jekyllrb.com/docs/installation/). Both the instructions provided by Jekyll and Bloc seemed straighforward enough:
* `$ gem install jekyl`
* `$ gem install jekyll-paginate`
* `$ gem install pygments.rb`

Well, that didn't work. Mainly because my Mac was running Ruby 2.0.0 and Jekyll requires version 2.1 or higher. So it took me a while to figure out how to get my machine switched over to a newer Ruby version.

The first time I got the error message - _ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory_ - I was very confused. I do all my coursework on my personal laptop. I am the sole admin. I should have perms for everything, right?? Apparently this was not the case. So I started searching Stack Overflow and poking around. Here are things I tried that did not work:
1. Gem install jekyll - error message as above
2. Rbenv init - command not found
3. Installed homebrew - successful installation!
4. Brew install rbenv init - fail (+ a couple of iterations that also failed)
5. Rbenv init - success (_I thought at the time, I was wrong_)
6. Gem install jekyll - error message as above
7. Rbenv init - seemed successful
8. Gem install jekyll - error message as above
9. Posted on Slack, and a student recommended I try rbenv local 2.4.1 - result: rbenv: version2.4.1 not installed
10. Tried gem install jekyll one more time just in case, same error message as above

So at that point I asked my mentor for help, and he suggested I run `$PATH` and `ruby -v` to see what was up. Turned out there were no shims showing when I ran `$PATH` indicating that rbenv may not have been correctly installed, and the `ruby -v` was still returning 2.0, so I hadn't managed to effectively update to a later version.

When I ran `curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash` I got an error: _Checking for rbenv' in PATH: /usr/local/bin/rbenv Checking for rbenv shims in PATH: not found The directory/Users/amyfarley/.rbenv/shims' must be present in PATH for rbenv to work. Please run `rbenv init' and follow the instructions_.

...so I ran `rbenv init` and got: Load `rbenv automatically by appending the following to ~/.bash_profile: eval "$(rbenv init -)"`. I had received that message previously, but didn't understand what it meant, and thought I'd successfully initiated rbenv. I hadn't. Finally I popped `eval "$(rbenv init)"` in the command line and sure enough, that propelled me forward.

I followed the rest of the steps and closed the window but when I reopened and did ruby -v, it still had 2.0.0 listed. I realized that apparently I need to run `eval "$(rbenv init -)"` every time and got `ruby -v` to display 2.4.1 and got the jekyll gem installed!

I have yet to figure out a way to permanently run ruby 2.4.1. Maybe someday I will!
