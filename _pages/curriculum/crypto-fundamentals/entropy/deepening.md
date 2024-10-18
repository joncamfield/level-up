---
layout: content-page
title: "Deepening : Working with Entropy" # name your lesson unit
author: #The public names / pseudonyms of the authors
parent: "Entropy and Password Security" #The titles of pages this links from
summary: "" #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/entropy/deepening/working-with-entropy/ #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Working with Entropy" #The name of this lesson
date: 2024-01 #Last updateddate in YYYY-MM
adids: Deepening # ADIDS element(s): Activity and Discussion, Input, Deepening, Synthesis
duration: 60-90 minutes #free form duration/time field
platforms: #Where relevant, what mobile or computing platforms does this apply to: Linux, Mac OS, Windows, Android, iOS

---


# Materials 

- This works best if you work through this collaboratively on a whiteboard, but you can also make a slide deck, or even do the calculations live on a spreadsheet.*

# Deepening


## Let's actually calculate some entropy!

To make things a bit easier, let's switch to numbers and pin codes for a bit, and explore a few routes one might take to try to guess a 4-digit code.

### Brute Force

A totally random number (0-9) would take 10 guesses to **guarantee** you guess the right number by "exhausting" the possibilities. When trying to guess a longer number (say, a 4 digit pin), you have to multiply by the number of digits, so a 4 digit pin takes 10×10×10×10, or 10,000 guesses.  For anyone who's forgotten the code to their luggage lock, this is what you're looking at.

Generally speaking, you have a chance at getting the "right" combination early, so you'd have to be incredibly unlucky to have to guess all 10,000 guesses - but even still, at 3 seconds a guess, you'd be at this for 8 hours straight.

### Informed Guessing: Dates

This is where understanding entropy really comes in handy.  Is that combination **really** actually random? Probably not. There's a good chance it's either a date or a year.  If it's a year, the first two numbers are probably either 19 or 20, and if it's 19, it's a good guess to work backwards from 99 down to 50. For 20, work up from 00 to 23. 

**This takes 10,000 guesses down to just 80** - 1×1×5×10 for 1950-1999 (1 guess × 1 guess × 5 guesses (5,6,7,8,9), × 10 guesses (0-9) = 50
plus 1×1×3×10 for 2000-2023 (and you could cut that down more by not trying numbers in the future) = 30

Now, of course, it could be a day/month combination in MMDD or DDMM

(*work through this with the participants*)

* What does month formatting look like from an entropy viewpoint? 01-12, so the first digit has 2 guesses, and the second has 10.
* Days go from 01-31, so the first digit has 4 possible options, and the second has again 10.
* So an exhaustive list of **all** MMDD options would take 2×10×4×10 or 800 more guesses, and DDMM adds another 800.
* Notably, there are further shortcuts here! you don't need to test days for 32,33,34, etc. 

So to guess all recent years, and all month/day combinations, you're still looking at 1680 guesses, which is a lot more doable than 10,000 - but even this is still more work than an exhaustive guess of all possible combinations for a 3-digit combo lock.

### Informed Guessing: Statistics

A (now-defunct) firm called DataGenetics put out a really [great post on PIN code entropy](https://web.archive.org/web/20180803052302/https://www.datagenetics.com/blog/september32012/), which makes the randomness of most PIN codes even more depressing with a dose of cold reality from leaked PIN data.  In their research, **"1234" accounted for 10% of all PIN codes by itself**, and "1111" brings in another 6%. 

Going through just 5 of most common from their 2018 analysis will net you over 20% of the PIN codes which were in the 3.5 million code leak, and you'll get 50% with onl 426 guesses.

Of course, going against any single specific PIN code, you never know (unless you're ready and able to try the full 10,000!), but broadly speaking, you have a one-in-four chance to guess a random pin code in 20 guesses, and another 1000 guesses gives you frighteningly better odds.

*The last discussion bit here puts this all together to painfully explain at length and with math you can use at home the famous ["Password Security" comic by xkcd](https://xkcd.com/936/)*

