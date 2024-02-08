---
layout: content-page
title: "Input : Entropy and You" # name your lesson unit
author: #The public names / pseudonyms of the authors
parent: "Entropy and Password Security" #The titles of pages this links from
summary: "" #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/entropy/input/entropy-and-you/ #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Entropy and You" #The name of this lesson
date: 2024-01 #Last updateddate in YYYY-MM
adids: Input # ADIDS element(s): Activity and Discussion, Input, Deepening, Synthesis
duration: 15 minutes #free form duration/time field
platforms: #Where relevant, what mobile or computing platforms does this apply to: Linux, Mac OS, Windows, Android, iOS
---


# Input 

In this lesson, a significant amount of Input is interwoven in the Deepening exercise as well, so this content serves as an introduction, and should be connected with the Activity exercise.

## Input Content 


Entropy is a small word for a big concept. Entropy is a measure of chaos, or the absence of order.

<!-- In physics, entropy is the Second Law of thermodynamics. Given the general state of the world, it may surprise you that life is amazingly anti-entropic. The complexities of all the systems working in any form of harmony to keep us all living on this planet is an amazing example of order - one in fact that requires a substantial portion of a star's energy output over billions of years to create and maintain.  In fact, the immense, raw, nuclear destruction ongoing inside that star is the "balance" of entropy that makes our order possible. -->

What does that have to do with passwords, or security, you ask?  If you've ever had to scribble your mouse across the screen for a few minutes to create a truecrypt or (more recently) veracrypt encrypted drive, you experienced this.  You were creating some chaos, some randomness... some *entropy* to make the drive more secure.  Why does that work?

Guessing facts about a city you've never visited is easy because cities follow many similar patterns -- and often legal regulations -- about how they exist, and as you understand more about basic patterns (does a city have streets) you can probably guess that it also has cars in it, and sidewalks, parking lots or garages, and so on. Language itself has a similar cadence, with rules of spelling and grammar (well, less so with English) and the study of information entropy in language by Claude Shannon is foundational to many security concepts today. Consider Shannon's original experiment here, as explained in [The Bit Bomb](https://aeon.co/essays/how-a-polymath-transformed-our-understanding-of-information):

	"Shannon expanded this point by turning to a pulpy Raymond Chandler detective story […] He flipped to a random passage […] then read out letter by letter to his wife, Betty. Her role was to guess each subsequent letter […] Betty’s job grew progressively easier as context accumulated […] a phrase beginning ‘a small oblong reading lamp on the’ is very likely to be followed by one of two letters: D, or Betty’s first guess, T (presumably for ‘table’). In a zero-redundancy language using our alphabet, Betty would have had only a 1-in-26 chance of guessing correctly; in our language, by contrast, her odds were closer to 1-in-2. " 

That difference, from 1-in-26 down to 1-in-2, is exactly the concept we're exploring! It's also a large part of how "Large Language Models" like ChatGPT work, but that's a [separate story](https://writings.stephenwolfram.com/2023/02/what-is-chatgpt-doing-and-why-does-it-work/). 
