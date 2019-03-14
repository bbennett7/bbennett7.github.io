---
layout: post
title:      "Getting a New Gem onto RubyGems.org"
date:       2019-03-14 03:52:33 +0000
permalink:  getting_a_new_gem_onto_rubygems_org
---


In light of having just published my first gem on rubygems.org, I want to revisit and walkthrough what I learned about the process of actually publishing my gem. We'll take a look at what the standard files of a gem look like, what information should go in each file (and what information is required), as well as the steps to actually publish your gem.




**What goes into a gem?**

A gem will be made up of three main parts - your files containing code, documentation files, and your gemspec file. The first of these will encompass your bin, lib, and test or rspec folders. The bin folder should contain the executable file that will run your program, the lib folder should contain all code that makes up the program (i.e., the code that will actually be executed by the bin file), and then the test or rspec file contain tests to ensure that your program is functioning as you intend and expect it to. 

The documentation files should include a README.md file, a LICENSE.mf file, possibly a NOTES.md file, and anything else that explains the installation, functionality and guidleines of your gem.

Lastly, there is your gemspec file, which details out information about your gem. This is where I'm going to focus in this post. The gemspec file will initialize with some information already in it, but it is up to the gem's author to ensure the information is correct. So, what is this supposed to look like at the end? In short, it will look something like the below - but we'll walk through this a bit more:


<a href="https://ibb.co/dBsvQGF"><img src="https://i.ibb.co/v1CWJZp/Screen-Shot-2019-03-13-at-4-05-54-PM.png" alt="Screen-Shot-2019-03-13-at-4-05-54-PM" border="0"></a>


How do you decide or know what is supposed to be in each of these, though? Here is a quick guide to what each is looking for:

* spec.name - This should be the name of your gem, and typically it matches the file name.
* spec.version - In your library folder, there should be a file titled "version" with a module and version number inside. In this space, put "YourModule::VERSION". Make sure that VERSION is in all caps, otherwise you will get an error message. 
* spec.authors - The name or identity of the creator(s)/contributor(s) of the gem, written like this: ["Name"].
* spec.email -  The email address for the creator of the gem, written like this: ["email"].
* spec.summary - Here you should add a brief description of your gem, written without quotes, likes this: q%{This is a brief description of your gem.}
* spec.description - This is a default option, but is not necessary. If you would like to add a longer description of your gem, you can do so here, with the same syntax as the summary: q%{This is a longer description of your gem, if the summary doesn't hold all of the info you'd like to give.}. If you don't need a longer description, you can delete this line. 
* spec.homepage - This is the url for your remote repository, NOT the homepage where your gem will live on rubygems.org. If you use github, it will be the github URL for the repository.
* spec.license - This will be the license your gem uses, such as "MIT".

You will then see the below in the default gemspec setup, which you can delete unless you are working on a private repository and want to control where the gem can be pushed. 


<a href="https://ibb.co/MSJV1PT"><img src="https://i.ibb.co/YQVkdf9/Screen-Shot-2019-03-13-at-4-18-45-PM.png" alt="Screen-Shot-2019-03-13-at-4-18-45-PM" border="0"></a>


At the bottom, you should list any other gems that your gem requires, written as:

     spec.add_development_dependency "gem1"
		 
     spec.add_development_dependency "gem2"

It should also be noted that in your Gemfile, you should list any gems that your program requires and list the source at the top, like this: 


<a href="https://imgbb.com/"><img src="https://i.ibb.co/6yp95KR/Screen-Shot-2019-03-13-at-4-39-49-PM.png" alt="Screen-Shot-2019-03-13-at-4-39-49-PM" border="0"></a>




**Pushing your gem to RubyGems.org**

After all of this is filled in with the proper information specific to your gem, we will be just about ready to actually get the gem out into the world. If you haven't already done so, sign up for an account at rubygems.org. In your terminal, run "gem build <your_file_name>.gemspec", which will actually build your gem. Make note of the text at the end after "File:", as you'll need this in a second.

Next, navigate to your profile on rubygems.org and click "Edit Profile", scroll to the bottom until you see a code snippet starting with "code -u". Copy and paste this whole code snippet into your terminal. This will set up your computer with your rubygems.org account. 

Now that you're set up with your account, in your terminal, type "gem push file_name", the file name here being the one you made note of just two steps earlier. You should then see that your gem was successfully registered, and it should appear under your rubygems.org account.


