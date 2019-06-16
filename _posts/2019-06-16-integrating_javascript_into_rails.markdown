---
layout: post
title:      "Integrating JavaScript into Rails"
date:       2019-06-16 16:30:56 +0000
permalink:  integrating_javascript_into_rails
---


Shifting from writing one language to another requires not just a shift in syntax and composition, but a total shift in thinking and approach. It can be difficult to make the switch, after envisioning and programming an entire site in one language, like Ruby on Rails. I found the toughest part to be identifying which parts should berefactored into JavaScript. Each language has its own strengths and weaknesses, and so the pros and cons must be weighed. It also helps to consider the website from the standpoint of the user, and to consider what behavior they might intuitiely expect your website to have.

For instance, for the purposes of meeting my specific project requirements, I chose to display each user's list of languages on their profile via javascript. This proved to be finicky, needing certain syntax for querying over other syntax that is different but serves the same purpose in order to work consistently. Since there is realistically a real-world cap on how large the languages database will ever be, and the number of languages that a user will "have", I would otherwise have kept it as standard Ruby. Alternatively I may have rendered the entire profile in JS.

It worked perfectly, however, for updating the "recent resources" section (part of the basic layout) immediately upon creating a new resource, without refresh. No issues with flashing, or not sticking, and it was nice as a user to see that updated in real time. 

The other areas that would lend itself well to JS, would be adding languages to user profiles, the coach selection process for a student, and a sorting process to view only resources of a certain language, or to search for a specific resource. These will likely be my next elements to refactor. 
