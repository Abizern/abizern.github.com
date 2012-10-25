---
layout: post
title: "UUID Strings with Cocoa"
date: 2012-10-25 11:52
comments: true
categories:
- OS X Development
- iOS Development
---

This used to be a thing until the iOS 6 and OS X 10.8 compatible
[NSUUID Class](http://developer.apple.com/library/mac/#documentation/Foundation/Reference/NSUUID_Class/Reference/Reference.html)
became available.

## New

This is how you can do it now:

{% codeblock UUID from NSUUID lang:objc %}
NSString *uuidString = [[NSUUID UUID] UUIDString];
// Generates: 7E60066C-C7F3-438A-95B1-DDE8634E1072
{% endcodeblock %}

## Old

Here's a method you can put in a class, with the correct ARC casts on ownership, that
returns a UUID. It's a fairly common technique, and you'll even see versions of
it where people have created a category on NSString for this.

{% codeblock UUID from a method lang:objc  %}
- (NSString *)uuidString {
    // Returns a UUID

    CFUUIDRef uuid = CFUUIDCreate(kCFAllocatorDefault);
    NSString *uuidStr = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, uuid);
    CFRelease(uuid);

    return uuidStr;
}

{% endcodeblock %}



And to use it:

{% codeblock UUID from a method usage lang:objc %}
NSString *uuidString = [self uuidString];
// Generates D5CB0560-206F-4581-AA25-1D6A873F3526
{% endcodeblock %}
