---
layout: post
title:      "How to Relate Two Instances of the Same Class"
date:       2019-06-10 02:20:42 -0400
permalink:  how_to_relate_two_instances_of_the_same_class
---


Upon beginning my Rails project, a website that would allow mentors and students to connect, I almost immediately ran into a problem: how do you model a relationship between two instances of the same class? A mentor and a student are both users, just different types of users. From a database standpoint, that would mean that a user belongs to a user, and also a user has one user, which just sounds like a recipe for disaster.

I tried several different things and ultiately decided to create two different types of user, one for a mentor and one for a student, because it worked well with the structure of my site. I started to wonder how a site like Facebook or LinkedIn, where the friends or connections are clearly the same type of user, were associated. I figure that for sites such as Instagram and Twitter, where it is a follow/follower relationship, it is more simple, since each of those can be considered a unique, one-way relationship. But was there a way to have a user to user relationship? Did each user have both their own "user" profile and a second "friend" profile, the former of which would have many friends and the latter of which would have many users.

Facebook and LinkedIn of course don't make this information public, and after combing through the HTML I still couldn't find much concrete. There is a general consensus though of how this is done, but with one interesting dispute still ongoing. The idea is to create a "Friendships" or "Connections" table, and connect users through this join table.

The unresolved question is: one line per relationship, or two? Does each friendship need just one entry in the tabe, containing the unique ID, user1, user2, and any other information you wish to store? Or does it need two entries, the first containing the unique ID, user1, user2, other info, and then also unique ID, user 2, user1, other info?

In theory, one entry is enough. It establishes the association between users that we are looking for. There are many reports though of issues with scaling this type of database, and of using it for anything else such as finding mutual friends. It is twice the number of entries, but can make actions such as listing an individual user's friends list much less costly. For smaller projects, learning purposes, or anything not intended to be taken to market, doing one entry per relationship would probably be just fine. But for anything intended as more than that, starting off with two entries is the safer option, and well worth the extra storage. 
