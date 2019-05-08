---
layout: post
title:      "Where to begin when debugging code"
date:       2019-05-08 01:11:37 +0000
permalink:  where_to_begin_when_debugging_code
---


I was recently asked, while demonstrating an API I had built, what I do when I get stuck. That is, what I do when I've written code that is behaving differently than I intended it to. I of course have my process as everyone does, but I had never had to articulate it - to break down step by step what my thought process and approach is to fixing broken code.

**1. If my code isn't doing what I want it to do, then what is my code doing?**
Especially in times when I am just *so sure* that the code I wrote should be working, I have to remind myself that if my code isn't doing what I expected it to do (not returning what I expected it to return, routing like I wanted it to, appearing or saving like I intended, etc.), it is still doing something. So what is it doing? Being able to answer this question almost always tells me what needs fixing.

**2. I now know what my code is doing, which isn't what I want it to do. Where is the error happening?**
Once I know what my code is doing, I use a combination of tools like my rails console, binding.pry and byebug, inspecting different objects using the raise method, to identify exactly what is happening at each step of my code. This allows me to see return values, parameters being passed, how methods behave, and more importantly, which of these are surpises and which are as I expected. I am able to pinpoint where in my code the bug is popping up. 

**3. I know where the error is occuring. What is causing the error?**
One of my favorite things about Rails is the amazing and detialed error messages that it gives us. Read your error messages!! Even if it seems like its not telling you what the error is, it is. I guarantee you once you see the problem and the solution, the error message will make total logical sense. Is the error message pointing to a method? An object? Mentioning params? Listen to your instincts here, and take this to the rails console. I like to recreate the problem, and then play around in the console (or use whichever tool is most appropriate) until I get something working that I can copy into my file.

