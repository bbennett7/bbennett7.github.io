---
layout: post
title:      "The importance of staying D-R-Y"
date:       2019-05-18 19:38:01 +0000
permalink:  the_importance_of_staying_d-r-y
---


I am just nearing the completion of my Rails project, which I used to build a code mentoring webapp. The idea is that, using opensource material, software engineers could sign up to become a mentor to a kid who might not otherwise have the opportunity to learn to code or know where to begin in the process. The mentors can add opensource materials, organized by language, for their student to read, and help guide the student in their computer programming journey. Students can track what they have read and rate the resources that are most helpful. 

I took the approach that I have taken up until this point, of getting my code working and then refactoring. This project was significantly more complex than the labs that I have done this with previously, and while the "red, green, refactor" approach is still best practice, I learned the importance of keeping a project D-R-Y rather than making it D-R-Y at the end. 

I saw, somewhat early on, that I would need certain helper and class methods, as well as certain show pages that were similar. There are two user models here - one for students and one for mentors - that had a lot of overlap. The multiple user model was a first for me so I was navigating something totally new, and wasn't sure how much I would have to keep totally separate vs. being able to create my own "student_or_mentor" type methods.

Turns out, I could still keep this almost as D-R-Y as I could if I were using only one user model. Never at the expense, though, of maintaining readability. I kept in mind to not go overboard with refactoring if I ended up with less legible code. A better approach for a future project, would be to create the pattern from the start - to create my own set of RESTful routes using a custom method like "student_or_mentor", and build everything using this custom pattern. This would allow the project to still be RESTful, but in a more useful way for the program. 


