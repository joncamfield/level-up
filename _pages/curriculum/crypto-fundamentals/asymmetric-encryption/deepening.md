---
layout: content-page
title: "Deepening : Encrypting Messages with RSA" # name your lesson unit
author: #The public names / pseudonyms of the authors
parent: "Asymmetric Encryption" #The titles of pages this links from
summary: "" #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/asymmetric-encryption/deepening/encrypting-messages #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Encrypting Messages" #The name of this lesson
date: 2024-0w #Last updateddate in YYYY-MM
adids: Deepening # ADIDS element(s): Activity and Discussion, Input, Deepening, Synthesis
duration: 90 minutes #free form duration/time field
platforms: #Where relevant, what mobile or computing platforms does this apply to: Linux, Mac OS, Windows, Android, iOS

---


# Materials 

- This works best if you work through this collaboratively on a whiteboard or flipchart
- Participants will need calculators - the simple calculator app on phones or laptops is sufficient.

This lesson first goes through the encryption and decryption process with pre-selected numbers, and then follows with a short explanation of how you can independently create the "right" numbers that work in this situation.

# Deepening

We are going to actually encode and messages, and learn a few bits of the math behind how public/private key cryptography actually works. 

*This lesson builds off of "Secrets Held, Secrets Revealed" in [Coincidences, Chaos, and all that Math Jazz](https://www.google.com/books/edition/Coincidences_Chaos_and_All_that_Math_Jaz/x-uQ2aiDveUC?hl=en&gbpv=1&dq=michael+starbird+secrets&pg=PA65&printsec=frontcover
) by Edward Burger and Michael Starbird.  If you want to diver deeper into this, I highly recommend it.*

The private and public keys in asymmetric cryptography - be that PGP, TLS certificates, or other places you'll find it - are numbers.  Very -- very large numbers.  And specifically, they are numbers with some very weird inter-connections, based on prime numbers (numbers like 11, but unlike 25, which can only be evenly divided by themselves and the number 1) and a calculation called "modular" arithmetic. 

To do this by hand, we are going to use very small numbers.  In real life applications, these are numbers with **hundreds** or even **thousands** of digits. (you can explore this with a few tools like pgpdump https://github.com/kazu-yamamoto/pgpdump !)


			~~
			7,11 and e=3

			p = 7
			q = 11
			n = 77
			phi n = 60
			e = 3
			encrypted = mod 33 ( (message)^7 )
			decrypted = mod 33 (encrypted ^3)
			~~

p,q = 11, 13
n = 143
ϕn = 120
e = 7
mmi = 103

Private key = n,  
Public Key = n, e


encrypted = mod _n_ ( (message)^_e_ )

decrypted = mod _n_ (encrypted ^_p or q_ )

message = 23
encrypted = 
	21^7 = 1801088541
	mod 143 (1801088541)
= 109

decrypted =
	109 ^ 11 = 2.580426405×10²²
	mod 143 2.580426405×10²²
-21 

1. 2 primes (p, q)
2. Multiply them together, note down the result - it will be part of both the public and the private key. (n)
3. With the same two primes, subtract 1 from each prime and multiply together the result. (Phi n or ϕn)
4. Select a third prime (e) which doesn't divide evenly into that result  (so, if the result is 65, 5, while itself a prime, is a bad choice). This third prime is the other part of your public key and will be used to complete your private key

5. There are some fancier math ways to get this final piece of the puzzle, which are required for numbers of a size large enough to actually provide any security. However, for today we're taking a much simpler shortcut, but still involving a core piece of the math - modular arithmetic.  

	Perhaps you remember when you were first learning division, and had "remainders" - divide 10 by 7 on a calculator, and you'd get 1.428571....  If you calculate remainders, you'd get 1r3 - 7 goes into 10 once, with 3 remaining.  With modular arithmetic, this remainder value is what we are trying to find - so 10 mod 7 is 3. 17 mod 7 (10+7) is also 3 - 7 goes into 17 twice (14), and the remainder is still 3.  It's also true that 13 mod 10 is 3. 103 mod 100 is 3 - it's kinda a funny tool, but in this weird use case, incredibly powerful for security.

	This is when we take a short break and remind ourselves that we're not becoming cryptographers right now - there is a ton of number theory behind how this works, where it doesn't, and more.  BUT - it is all actual math, with steps one can follow by hand - that underpins all of this.


ANYHOW - We are looking for an integer - a number with no decimals, that multiplies with e, that Phi n - the number from step 3 -  modulo this is 1.  There are some fancier math shortcuts to find this, but we're going to take the simple route here. 


* Take the "Step 3 number" and add 1
* Divide that by e. If we get a simple integer, that's our answer.  The "add 1" step here is to ensure that we find the mod = 1 result.
* If we got a number with decimals, we keep going - each step from here multiplies the "step 3 number" incrementally - 2x, 3x, 4x, etc., then adds 1, and then divides by e - until we get a plain integer.  With the numbers 7 and 120, here is the process:

Try 1: (120 + 1)/7 121/7 = 17.2857...
Try 2: (120 * 2 +1) / 7 = 241/7 = 34.428571429
Try 3: (120 * 3 +1) / 7 = 361/7 = 51.571428571
Try 4: (120 * 4 +1) / 7 = 481/7 = 68.714285714
Try 5: (120 * 5 +1) / 7 = 601/7 = 85.857142857
Try 6: (120 * 6 +1) / 7 = 721/7 = 103 ...WOOT!

BINGO! The number we're looking for is 103.  This number will also always itself be smaller than the number we are dividing in to, because that would simply cause us to loop over again - so if you kept going, you will find more numbers that work, but it is this first one, which is less than the number you're dividing in to from Step 3, which is the one that successfully completes the math. 

For anyone following along at home, this is called the "modular multiplicative inverse".





https://www.google.com/books/edition/Coincidences_Chaos_and_All_that_Math_Jaz/x-uQ2aiDveUC?hl=en&gbpv=1&dq=michael+starbird+secrets&pg=PA65&printsec=frontcover

https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/
https://nhoyle-unsw.github.io/learn-encryption-with-python/Modular-arithmetic.html
https://doctrina.org/How-RSA-Works-With-Examples.html
https://doctrina.org/Why-RSA-Works-Three-Fundamental-Questions-Answered.html
https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm#Example
https://ccom.uprrp.edu/~humberto/very-small-rsa-example.html
