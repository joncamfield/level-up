---
layout: content-page
title: "Deepening : Hashes" # name your lesson unit
author: #The public names / pseudonyms of the authors
parent: "Entropy and Password Security" #The titles of pages this links from
summary: "" #A 1 P summary that will go on listing pages and at the top of this page
permalink: /curriculum/crypto-fundamentals/hashes/deepening/hashes/ #The full URL of this, for its primary parent page, e.g. /curriculum/safer-browsing/anonymity-and-circumvention/activity-discussion/offline-circumvention/
breadcrumb: "Working with Entropy" #The name of this lesson
date: 2024-07 #Last updateddate in YYYY-MM
adids: Deepening # ADIDS element(s): Activity and Discussion, Input, Deepening, Synthesis
duration: 60-90 minutes #free form duration/time field
platforms: #Where relevant, what mobile or computing platforms does this apply to: Linux, Mac OS, Windows, Android, iOS

---


# Materials 

* Participant who don't want to use the command line tools should download and install QuickHash [Download Link](https://www.quickhash-gui.org/downloads/) [Source Code](https://github.com/tedsmith/quickhash). QuickHash provides a [quick guide for installation](https://www.quickhash-gui.org/about-quickhash-gui/faqs/#qaef-1643) across the different platforms.


# Deepening

All modern operating systems have built in hash creation/verification tools, but they are command-line based. In this session, we will use a graphical tool called QuickHash, but we will also provide command-line options for users who are willing to use the command line and/or don't want to download additional software.

## File Hashing

Let’s get hands on and create and verify some hashes - first up, we'll verify the hash of the quickhash download file itself!

*Note that ideally, you'd use one of the built-in tools below to verify QuickHash, as you're functionally trusting quickhash to verify itself here*

* On the QuickHash [Downloads](https://www.quickhash-gui.org/downloads/) page, click the name (not the download button) of the version you're using, which should take you to a page [like this Windows download page](https://www.quickhash-gui.org/download/quickhash-gui-v3-3-4-for-windows/).
* Find the hash values at the bottom of the page. 
* Open QuickHash
* Select the File tab
* Choose which hash you want to compute - in this case, the quickhash downloads pages provide SHA-1 and SHA-256 hashes, so choose one of those.
 Select the quickhash zip file download
* Compare the hash it created with the hash from the website - you can review it manually, or for better accuracy, paste in the value from the website in the "expected value" field (replacing the '…')

Hopefully the values matched! If not, verify you used the same hash algorithm, and are on the download page for both the operating system (Linux, Apple/OSX, Windows) AND version that you downloaded.

## Text Hashing

* Open QuickHash
* Select the Text tab
* Choose which hash you want to compute
* Type in text to the text box (*if you constantly get errors, type ... in the Expected Hash box or restart QuickHash*)
* See the hash value in the the dark grey box below.
* Try a few common strings like Password vs password vs Password! and see how different the hash values are.
* Try a few different algorithms to see how they look, and how long they are (independent of how long your text is!)

## Command Line Tools

### Windows

In Powershell (v4 or above), you can use the Get-FileHash 'cmdlet' for producing hash values.  For tilres 

`Get-FileHash C:\Users\user1\Downloads\Contoso8_1_ENT.iso -Algorithm SHA384 | Format-List`


Powershell unfortunately does not provide a simple way to compute a hash for a string, but there is a workaround, setting a string as a variable in what Microsoft calls a "stream":

```
$stringAsStream = [System.IO.MemoryStream]::new()
$writer = [System.IO.StreamWriter]::new($stringAsStream)
$writer.write("FOOBAR")
$writer.Flush()
$stringAsStream.Position = 0
Get-FileHash -InputStream $stringAsStream -Algorithm SHA384 | Select-Object Has
```

Microsoft provides [PowerShell GetHash documentation](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.4)

### OSX

Terminal

### OSX and Linux

In your Terminal program or directly in a command line, you have a variety of options in both OSX and Linux to check hashes. The most flexible is the openssl tool (it can also do a wide variety of other cryptographic tricks!).

You can get a list of all the hash functions openssl supports with

`openssl dgst -list`

To get a hash of a short text string, use this command, replacing FOOBAR with your text (and selecting the hash, here using SHA-3)

`printf FOOBAR | openssl dgst -sha3-256`

To get a hash of a file, use this command, replacing FILENAME with the path to the file you want to hash (and selecting the hash, here using SHA-3):

`openssl dgst -md5 FILENAME`

*Of note, in Ubuntu, you can also install **nautilus-gtkhash** to add a right-click menu tab that will generate hashes for you in the file manager GUI.*
