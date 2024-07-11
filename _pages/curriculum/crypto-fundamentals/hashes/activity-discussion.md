---
layout: content-page
title: "Activity-Discussion : Simple Hashes in Everyday Life" # name your lesson unit
author: Jon Camfield #The public names / pseudonyms of the authors
parent: "Hashes" #The titles of pages this links from
summary: "This activity runs participants through a very simple, but real-world example - the checksum of a credit card." #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/hashes/activity/hash-creation/ #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Hash creation" #The name of this lesson
date: 2024-07 #Last updateddate in YYYY-MM
adids: Activity and Discussion # ADIDS element(s)
duration: 30 minutes #free form duration/time field

---

# Materials to Prepare

* Participants will need calculators (the built in one in smartphones is sufficient)
* You should provide ("sample" credit card numbers using [https://www.freeformatter.com/credit-card-number-generator-validator.html](https://www.freeformatter.com/credit-card-number-generator-validator.html). You may want to print out some worksheets if you don't have a presentation or whiteboard option.
* If participants want to test this with their personal credit card numbers, remind them to tear up any paper with their number on it.
* A whiteboard or presentation is helpful but not required


# Running the Activity

*This activity runs participants through a very simple, but real-world "hash" example - the checksum of a credit card.  It is less robust than the hash functions the rest of the lesson will focus on, but provides a tangible example.*


## Checking in on credit cards

If you've ever put your credit card number in a form and gotten an error before you even added the date or security code, this is how that happens. Almost every credit card number uses what's called the [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm) as a self-check.  


We can test this ourselves!

*It's worth noting that this alone only lets you verify numbers (and generate test numbers), and indeed it's an open standard. Without correct expiration dates, name, and security codes this is absolutely useless for payment activity.*


* Take (almost) any credit card (some cards use a different formula, but any "Visa" or "MasterCard" will work). 
* For the purposes of this activity we have some test numbers we can validate.
* Ignore the last digit in the credit card number for the moment - it should match the answer after the rest of the steps below.
* Reverse the order of the rest of the numbers of the card
* Multiply every other digit starting with the first (so, odd digits - 1, 3, 5, etc.) by 2.
* Subtract 9 from any numbers higher than 9
* Add all the numbers together
* With that sum, calculate the number you'd need to add to get to the next multiple of 10 (e.g. if you end up with 121, the next multiple of 10 would be 130, so the number you're looking for is 9). Yes - this is using modular arithmetic, which we learned in [Asymmetric Encryption](/curriculum/crypto-fundamentals/asymmetric-encryption/)
* This number should match the number we ignored in the first step!

More detail on credit card checksums is available at [https://www.freeformatter.com/credit-card-number-generator-validator.html](https://www.freeformatter.com/credit-card-number-generator-validator.html)

# Leading the Discussion

This is a simple check that provides a way to validate a set of data.  While credit cards are just a short string of numbers, a more complicated process could check for errors or typos in other formats, including text or even files.

Can participants come up with ideas where this might be useful? 

If they are struggling, suggest things like copying or downloading files over bad connections, or checking to see if a file is a duplicate of another file.

What if a system could provide more than just a format check, but a guarantee that a string of text or a file was - or was not - the same as another, or hadn't changed? 

Why would you want something like that?


