---
layout: post
title:      "The !@#$%^&* of Programming: Regular Expressions"
date:       2020-06-06 21:13:53 -0400
permalink:  the_at_and_of_programming_regular_expressions
---


Before the first project due for Flatiron, there were many concepts that was tough to understand such as the self keyword, object relationships, and metaprogramming concepts. For me there is one concept that I have not fully understood yet, which is the regular expressions, or regex for short. 

Regex is such a tough concept to grasp but at the same time it is a very power tool to search strings for a certain pattern. The history of regex is pretty hefty but it started off with a person in 1950. He was Stephen Kleene, an American mathematician. He called “his notation for expressing the algebra of regular sets” as regular expression[1]. Through the years, this culminated into a concept in programming that searches for patterns. I always thought math and programming goes hand in hand. I am not a pro at regular expression but I will show an example about how powerful this search tool is.

For instance we have a sentence:

	“Hello World!”
	
To select the space in between the two words, I would type in between two forward slashes:

	/\s/
	
That is easy enough. Now how about just the exclamation point in the string? If I do this:

	/\W/
	
I will get both the space and the exclamation point. Easiest way to select the exclamation point is to put it in a bracket like this:

	/[!]/
	
This was only a simple example of using regex to select patterns. In my CLI project, I used a regular expression to pull html tags that just became plain text out of a string. It just did not look right with them in. And this was how I did that:

`/<("[^"]*"|[^'">])*>/`

I somehow came to this conclusion after countless hours searching the web. I am not a pro at handling regular expressions yet but I will try to master this concept even if it takes a very long time. I believe this is a very powerful concept that will help me in the long run. (And I love hard concepts!)



[1] “Regex Legends: The People Behind the Magic.” Flagrant Badassery: A JavaScript and regular 	expression centric         blog. 13 January 2008. 6 June 2020. Retrieved from http://blog.stevenlevithan.com/archives/regex-legends#:~:text=In%20the%201950s%2C%20distinguished%20American,the%20algebra%20of%20regular%20sets.

