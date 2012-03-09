---
date: '2010-02-07 18:52:32'
layout: post
slug: three-ways-of-excluding-files-from-git
status: publish
title: Three ways of excluding files from git
wordpress_id: '278'
categories:
- Mac Development
tags:
- 365git
- config
- exclude
- git
- ignore
- xcode
---

Almost every git user knows about adding a `.gitignore` file to their repository to control the visibility of files and folders. This per project configuration will apply to all repositories of the same code base. But it’s not the only way. I’m going to tell you how to get [git](http://git-scm.com) to ignore files on a per computer and per repository basis. These could be better choices in some circumstances.

There are three types of exclude files; from highest to lowest order of precedence they are:


## Per Project: .gitignore file in the repository


This is the usual way of adding an ignore file. Call it `.gitignore` and save it to the root of your project to apply to all the files (you can add different `.gitignore` files in subdirectories where they have lesser scope). It is a part of the repository, so it will need to be `git-add`ed and committed for each change. This is useful for repositories that are passed around with others who may not have a per computer exclude file, or when there are project specific files that need to be taken into account. Even easier if you have per computer file, you can copy it straight in to your project with a simple `cp ~/.gitignore .gitignore` and edit to handle your specific requirements.


## Per Repository: in .git/info/excludes


You can exclude files on a per repository basis by editing the `.git/info/excludes` file in your repository. (Why it takes it from this location rather than `.git/config` I don’t know: add it to the list of git annoyances). These exclusions (or inclusions, you can override the higher level exclusions by prepending `!` to lines that you want to include) are not shared with the working directory, so they only apply to that particular repository. This is useful when you have particular requirements because of your workflow or machine setup.


## Per Computer: through ~/.gitconfig settings


There should already be a `.gitconfig` file in your home directory. This is where the global setting for your git installation are stored; such as the user’s name and email address. Within this you can set a path to an excludes file that will apply to all git repositories on the computer in the same way as the name and email defined in this file apply to all repositories.

For example: Most of what I do is in [Xcode](http://developer.apple.com/tools/xcode/) so I have the following ~/.gitignore file




# ~/.gitignore

*.DS_Store
*.pbxuser
*.mode1v3
*.mode2v3
*.perspectivev3




And in my `.gitconfig` file under the `[core]` section I have added the path to this file for the `excludesfile` key. (If you’re sharp eyed, you’ll notice that I don’t have an exclusion for `/build`. That’s because I don’t keep my products in my project directory, but that’s for a different post).




<snip>…
[core]
editor = /usr/bin/see -w -r -o new-window -j ‘git editor’ -m gitCommit -g 1:0
excludesfile = /Users/abizern/.gitignore
<snip>…




Now, I have a standard set of ignores that apply to all my git repositories on this machine without me having to add a specific `.gitignore` file to each one. This is probably most useful if you create a lot of repositories for yourself, but I recommend it to everyone. It’s lowest on the precedence scale and provides a neat catch-all.


## Summary


Most of the time the first solution is quite adequate, having exclusions with a repository that is likely to have a public face is probably the most effective way of managing file visibility. But, as with most of git, there are ways of handling edge cases. You just need to know that they are there.



## Related Reading


If you liked this post, have a look at my [365Git](http://365git.tumblr.com/) site for more tips.

**REFERENCE:** the [gitignore](http://www.kernel.org/pub/software/scm/git/docs/gitignore.html) man page.
