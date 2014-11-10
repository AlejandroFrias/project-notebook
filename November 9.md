# Design notebook for week ending November 9, 2014

## Description

I've been spending most of my time researching existing techonologies. Xtext with Xtend for eclipse looks promising. There seems to be ways to take in user input in the form of text by making an eclipse plugin. And that eclipse plugin has access to the cursor, both its position and the ability to change its position. Testing still needs to be done. My DSL might be moving towards a DSL for creating the plugin commands that move the cursor and paste in snippets or templates.

This has taken many hours (at least 7 over the weekend plus sporadic work throughout the week). I wasn't able to write the test cases I wanted yet since at first the research was making it look like I'd have to change my domain significantly.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

Right now, I need to make sure I there will be a feasible way to implement what I want. As I'm discovering what is in the realm of possibility, the domain for my DSL is narrowing. Then I'll be able to focus on a reasonable subset of design decisions. It's looking more and more like I'll be creating a DSL internal to java that is used for the creation of a specific kind of plugin for template/snippet generation from english text commands and for commands to navigate within a file (or multiple files). I want to see how I can get user input the way I'd like. The goal is to find a way to take in user input in the form of text (that could eventually be generated using a speech to text service) for running various predefined commands. But the user should also be able to click and type like normal in the text editor. I believe eclipse plugins is the answer, but if it isn't the host language and kind of design decisions will be very different, so I'm holding off on that until I can confirm if this is the way to go.


**What questions do you have for your critique partners? How can they best help
you?**

Do you know of anyways to do what I want? Or any technologies I should look into?

Also, as possible user, would like the ability to have english commands for things you do when writing code, like "go to the body of the main function" that could automatically take the cursor to the right file and line number or "for loop from 0 to 10" automatically generating an appropriate for loop for the language you're working in?


**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

7 hours I can easily account for that were dedicated to the project (not including project-notebook work). There have been lots of time between other activities where I have been brainstorming and thinking about the project.


## Post-critique summary

## Post-critique reflection
