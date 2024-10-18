---
layout: content-page
title: "Input : Learning about Hashes and their Limits" # name your lesson unit
author: Jon Camfield #The public names / pseudonyms of the authors
parent: "Hashes" #The titles of pages this links from
summary: "" #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/hashes/input/whats-a-hash/ #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Learning about Hashes and their Limits" #The name of this lesson
date: 2024-07 #Last updateddate in YYYY-MM
adids: Input # ADIDS element(s): Activity and Discussion, Input, Deepening, Synthesis
duration: 45 minutes #free form duration/time field
platforms: #Where relevant, what mobile or computing platforms does this apply to: Linux, Mac OS, Windows, Android, iOS
---


# Input 

## What are Hashes?

Hashes provide "one-way" functions that create a unique code from any specific input, from a password to a file. That unique code is only created from the specific input you gave it, with no modifications allowed, and using the same hash function on the same input will always create the same unique code as output.  BUT - and this is the one-way part of it, you cannot "go backwards" and take that unique code and figure out the original input.

As we go through the rest of the lesson, we'll find a few exceptions to these rules, but this is the theoretical goal of a hash function.

## Everyday uses for hashes

Let's dig in to a few common places hashes are used, and what work they are doing for us.

### Credit cards

As you explored in the activity, credit cards use a basic form of hashing, called a checksum.  These are not resilient against malicious attacks, but provide simple ways to detect accidental errors - like a typo on a credit card payment form, or a file that has an error in it.

### Passwords

Hashes are - or at least should be - fundamental to websites and passwords. Websites don't actually store your password; as doing so opens up a ton of risk from bad employees to huge problems if their password database gets stolen.  What they actually store is a cryptographically secure hash of the password. This lets them store a code that's not easily reversible back to your real password, but also lets them re-run the same hash on the password you provide when logging in, and make sure it matches the hash they have stored. 

This is notably how [HaveIBeenPwned](https://haveibeenpwned.com/) is able to safely track and correlate password breaches and their impact.

Hashes for passwords are great, but insufficient by themselves for "common" passwords. 

Common and obvious passwords - not just password1, 12345, and so on, but also the most obvious substitutions like P@assw0rd - have all been exhaustively explored.  As mentioned in the article below, if you take a hash (using md5) of P@assword and google search it, you get hundreds of results from "reverse" hash databases which have pre-compiled hashes for known common passwords, making simple hashes less secure for common passwords - and if you've already gone through the [Entropy]() lesson, you'll know just how common common password are. 

Additional detail: https://www.troyhunt.com/we-didnt-encrypt-your-password-we-hashed-it-heres-what-that-means/

And as always, XKCD has a great example of this with their [password crossword](https://www.explainxkcd.com/wiki/index.php/1286:_Encryptic) - which someone made into a playable game based on an Adobe password leak: https://zed0.co.uk/crossword/ 

### Downloading software

When you want to be extra sure that the file you downloaded is the same one you got, you can (and are often encouraged to) "check the hash" or "review the checksum" - these are hashes provided on the download side which you can also then run a local hash program on the file, and check that they match.  If they don't, something's gone very wrong. 

Common: Software! This is the mechanism behind “checksums” in downloading software
Ubuntu provides hashes and PGP https://ubuntu.com/tutorials/tutorial-how-to-verify-ubuntu#1-overview
Tor goes a step further and uses PGP: https://support.torproject.org/tbb/how-to-verify-signature/


### PGP signatures

When you choose to "sign" an email or create a signature on a file with PGP, you're actually using a hash as well.  The program creates a hash of the document as it exists, and then you essentially reverse-encrypt that hash. As you learned in [Asymmetric Encryption](/curriculum/crypto-fundamentals/asymmetric-encryption/), normal PGP encrypts using the recipient's public key, guaranteeing that only the person with that corresponding private key can decrypt it.  Signing in PGP instead encrypts using *your* *private* key (don't worry, it's safe!), so that anyone with your *public* key can "decrypt" it. 

Obviously that's useless for confidentiality, but if you wanted to be able to, say, prove that a document was exactly as you intended it to be, and to guarantee that exactly and only you were claiming that proof, a combination of a hash (to verify the exact state of a document and its contents) with an encryption system flipped over such that anyone could verify that the owner of a specific private key had encrypted that hash - becomes oddly powerful and useful.


## Attacks against Hashes

We started with defining hashes as (1) one way - you cannot discover the original value from the hash of it, and (2) unique - exactly one input creates exactly one output.  These are only ... mostly true. Let's talk about a few of the attacks against hashes.

### Rainbow Tables

As we discussed in the password section above, if you can guess the input to the hash, you can verify you "got" the right answer if hashing your guess matches the stored hash value. 

In fact, people have essentially "brute forced" many common passwords and made extensive lists, called [Rainbow Tables](https://en.wikipedia.org/wiki/Rainbow_table). Luckily, most websites add what's called a "salt" to each password, which adds a non-secret value to the password, rendering pre-computed rainbow tables useless by changing the hashed value and thereby changing the hash itself.


### Collisions

In the world of hashes, a collision means two **different** inputs create the same 'unique' hash output.  Obviously that can be very dangerous if you're relying on the hash to guarantee, for example, that you provided a specific document like a contract where you refused to sign, and someone can create a different document with the same hash that looks like you did sign.

Collisions are - thankfully - rare, and using more updated hashing tools dramatically reduces the possibility of a collision being created. We we'll get to in the final section, there are different algorithms available to create hashes.  One, which is still commonly used, is called md5, and it has been found to be vulnerable to (complicated) collision based attacks - you can see a [demonstration and code here](https://www.mscs.dal.ca/~selinger/md5collision/). It can still be useful, as it creates short output strings, but must be considered less secure than some other options.

## Hash Functions

For normal files, passwords, and text, the most common hash algorithms you'll see are likely MD, SHA-1, and SHA-2 (also often called SHA-256), and more recently, SHA-3.  Of these, MD5 as mentioned suffers from (relatively) easy collisions, and SHA-1 has been more recently [found vulnerable](https://www.zdnet.com/article/sha-1-collision-attacks-are-now-actually-practical-and-a-looming-danger/) to some collision attacks.  As of publication date, SHA-2 remains largely secure, and SHA-3 is even more secure.

[Wikipedia](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms)maintains an article with a chart of the security of these most used hash algorithms.

### A note on image hashes

Images (and other media) are particularly challenging to "hash" in the same way we use hashes for absolute precise matching of other types of files. Changing a pixel in an image is very different from changing a word in a document. If you are trying to use hashing to match images, any adversary (as well as innocent image processing/resizing tools) can create a totally different hash for, perceptually, the same image.  Researchers have built creative tools to better "hash" an image based on how it looks rather than the much more fragile file architecture hiding behind it.  

Images hashes provide a way to track the spread of harmful imagery including NCII and CSAM, but are also subject to collision attacks and weaknesses, and researchers are finding potential ways to "reverse" perceptual hashes so cannot be used as absolute guarantees.
