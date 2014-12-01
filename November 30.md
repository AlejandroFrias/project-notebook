# Design notebook for week ending November 30, 2014

## Description

Last week I had a very preliminary working version, like halfway between a proof of concepts and buggy prototype.

This past week had been dedicated to documentation, testing, and refactoring. I've also spent time making it easier to use. Instructions for use are in the Readme. The newest feature is that the default location to save the generated plugin is the very folder you need to save it to anyways (assuming OSX and default installation of Sublime Text 3).

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I need to deal with optional groups and some other interesting bugs that arise from interactions of Parser Objects that make matching the input commands ambiguous. Also some wierd spacing things. For now I've removed optional groups in the regex for the Parser Object, but I want to add those back.

Only lower case words are allowed, and no apostrophes. I want to change that, but it makes parsing more difficult.

I really want people to collaborate on making a series of commands. So I need import statements. I have only thought about it. I haven't attempted to implement it yet. That is the next major feature that will require design decisions. It will also require some kind of recursive prepocessing.

**What questions do you have for your critique partners? How can they best help
you?**

Are you able to install and use it easily enough? I hoped that it would be easier now to start creating Translator Objects and get a working plugin foing.

Also, does the syntax highlighting word better?

I'd like feedback on the documentation. Is it clear enough what you need to do to use it?

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

Not sure. I've been working on it throughout break while doing other things. I'd say at least 15, probably more.

## Post-critique summary

Documentation was poor, to say the east. That was the major feedback that needed attention. 

## Post-critique reflection

I agreed and have since put in the testing and documentation.
