---
layout: post
title:      "Encryption and Hashing, or, How Your Pet's Name Becomes a Secure Key"
date:       2019-04-12 23:53:27 +0000
permalink:  encryption_and_hashing_or_how_your_pets_name_becomes_a_secure_key
---


While working on my Sinatra portfolio project, in which I built a webapp where users can create an account and store their bucketlists and travel destinations, I became very intrigued at how a few simple lines of code like "has_secure_password" and "require 'bcrypt' " make a user's password, typically a string short enough that a user can remember off the top of their head, into something that hacker's with massive computing power can't crack without serious luck on their side.

Computers have gotten exponentially faster since they first were introduced, which makes day to day life easier in almost every way. It also makes it faster and therefore easier for hackers to run a dictionary of common passwords against a stolen password database. Enter hashing and encryption. 

The term hashing comes from the cooking term, where hashing a food means to slice it up and mix it around. **Hashing functions** are algorithms that act similarly to this, in that they take the actual binary code of a password, and "hash" it. The result is a user's password returned as an incomprehensible string of hexidecimal values. To avoid two user's with the same password ending up with identical hashed passwords, "salt" is added to each password prior to hashing. **Salt** is a random string, unique to a user, that is added to differentiate it from a different user's identical password. The resulting hashes will look nothing alike.

**Bcrypt** is one of the most common hashing algorithms used. It allows you to set a **cost**, which is the number of times the hashing algorithm is run on the password. This cost allows for scaling - as computers get faster, Bcrypt can get slower. The higher the cost, the more expensive the password is for someone to hack. The default cost on Bcrypt is 12, meaning 12 iterations of the algorithm will run on any given password. Bcrypt also automatically generates user specifc salt and adds it to passwords for added security.

The result of using the Bcrypt hashing algorithm is an encrypted password - something that can only be unlocked with the proper username and password combination. Entering a password off by even one character would result in an entirely different looking hash, so knowing one correct password to an account would give absolutely zero indication of what any other encrypted passwords are pre encryption, even an identical password. 

You can check out the code for the Bcrypt gem [here](http://https://github.com/codahale/bcrypt-ruby) to see what goes into the actual algorithm. 
