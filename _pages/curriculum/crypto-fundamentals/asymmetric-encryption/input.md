---
layout: content-page
title: "Input : Understanding Asymmetric Encryption" # name your lesson unit
author: #The public names / pseudonyms of the authors
parent: "Asymmetric Encryption" #The titles of pages this links from
summary: "" #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/asymmetric-encryption/input/encryption/ #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Understanding Asymmetric Encryption" #The name of this lesson
date: 2024-02 #Last updateddate in YYYY-MM
adids: Input # ADIDS element(s): Activity and Discussion, Input, Deepening, Synthesis
duration: 60 minutes #free form duration/time field
platforms: #Where relevant, what mobile or computing platforms does this apply to: Linux, Mac OS, Windows, Android, iOS
---


# Input 

## A Very Quick History of Encryption

Simple "Replacement" codes, (changing A to M, B to N, C to O and so on) like *Caesar ciphers* are easily broken, even if you make them more complex by using letters instead of numbers. Still, they were famously used by [Julius Caesar](https://en.wikipedia.org/wiki/Caesar_cipher) to obfuscate his correspondence -- but nowadays appear as games in newspapers and magazines to be solved by anyone.

Obviously, we will need something a bit more powerful for modern secure communication! 

Symmetric encryption filled this gap by itself for decades.  It is very powerful, and widely used even today -- but by itself, it has some serious limitations. 

One version of this is what’s referred to as a “One Time Pad” (OTP) - which, if done to very exacting standards, is still considered “unbreakable”.  https://en.wikipedia.org/wiki/One-time_pad 

Unfortunately those exacting standards are all but impossible to do in practice, and certainly at any scale. An OTP is effectively a long string of completely, truly random characters, which you “add” to the characters of your own message, to create what looks like gibberish. The recipient has to use the exact same pad (and know exactly where to start using it) to decrypt it, and the pad of random characters has to be at least as long as the message.

This becomes a bit of a chicken-and-egg problem, as to send a message using OTP, you first have to send the OTP content itself in an absolutely secure way.

The rest of symmetric key encryption - which just means a type of encryption where both the sender and receiver must have some sort of shared secret before they can encrypt, shares many of these same challenges -- **how to get those first secret keys shared**, and what to do if you need to replace them?

## What does a better encryption system look like?

*Brainstorm with participants some features of an encoding systems - what protections it provides, how usable it is, and so on.  Some key points to pull out of this brainstorm:*

* Only I should be able to read messages sent to me
* It should not be simple to break or reverse-engineer, even by a powerful computer 
* This rules out any “simple” substitution cipher like the ones discussed above
* People communicating shouldn’t have to exchange a secret code before they can exchange secret information
* Additional points that are useful for building on later:
* I should be able to verify who sent me a secret message
* The type of information I'm sending and other “metadata” should also be hidden 

## What Asymmetric Encryption is

public key, private key

