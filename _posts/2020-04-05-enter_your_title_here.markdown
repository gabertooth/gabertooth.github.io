---
layout: post
title:      "Reg Ex Begginners Guide"
date:       2020-04-05 15:53:48 -0400
permalink:  enter_your_title_here
---


Regular expressions are a powerful way of building patterns to match text. However they can be difficult to learn at first and the syntax can look visually intimidating. This is directly quoted from Dataquest, “As a result, a lot of students end up disliking regular expressions and try to avoid using them, instead opting to write more cumbersome code.” It is this exact reason that I decided to focus this post on regular expressions. I will try to simplify the learning into a 10-20 minute read. I hope you enjoy. 

Benefits of learning regex:  
* Once you understand how they work, complex operations with string data can be written a lot quicker, which will save you time.  
* Regular expressions are often faster to execute than their manual equivalents.
* Regular expressions are supported in almost every modern programming language, as well as other places like command line utilities and databases. Understanding regular expressions gives you a powerful tool that you can use wherever you work with data.

The main thing to keep in mind is the fact that you will not be able to remember and memorize the intricacies of every regex. Instead, you will want to understand the extent of the capabilities and know where to look for the details online.

The Basics:  

* Pattern: The text or symbol pattern we are looking for in our data  
* Match: A matching set of string/numbers/characters within our data where the matching pattern is found  
* Re: package or module contains a number of different functions and classes for working with regular expressions.
	re.search(the regex pattern, data/string): returns None if not found and Match if found  
* Set: allows to specify two or more characters that can match in a single character’s position    

     * Sets are useful when we want to be able to have the search pick up both lowercase and uppercase, in addition when there is more than one right thing we are searching for. 
* In addition to this we can then use {} aka curly brackets to specify a repeated pattern with the number inside it, x, the number of repeating times the pattern shows up. This simplifies our code.  

     * When specifying the number of times the quantifier repeats itself, like so a{3,5} think of it as when selecting a lists range. So the above {3,5} would be three, four, or five times of a repeating. Same holds true for say something like this a{8,} would be 8 or more. Below are a few very common numeric quantifier.  

* To match the substring "[pdf]", we can use backslashes to escape both the open and closing brackets: \[pdf\].  

     * Due to the escaping backslashes we need to use raw strings. For example when say hello\b world shows up in code we would need to use a raw string in order to account for the \b. This will esnure our regex does not break!
Capture groups. Capture groups allow us to specify one or more groups within our match that we can access separately.  

* Negative Character Classes: Negative character classes are character classes that match every character except a character class.   

* Word boundary anchors: \b is the syntax where it matches the postion between a word character and non-wrd character, or a word character and the start/end of a string.   
 
* Beggining and end anchors: anchors match something that isn't a character, as opposed to character classes which match specific characters.  

* Flags are used to specify that our regular expression should ignore case. An argument flag is available in the re.search method. The most common case is contained in re.I so pass this in and you most likely will be covered.  

