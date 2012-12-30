---
layout: post
title: "Correcting Brace Layout"
date: 2012-12-30 11:09
comments: false
categories:
- Ruby
- Objective-C
- General Programming
---

I wrote a [small rubygem](http://abizern.org/fixbraces/) called _fixbraces_ to
move the opening brace of a conditional to the same line as the opening
statement.

So now I can correct all the Xcode generated stub that look like:

    - (void)someMethod
    {
        // some code here
    }

Into my preferred format:

    - (void)someMethod {
        // some code here
    }

Which fits with my personal coding standards.
