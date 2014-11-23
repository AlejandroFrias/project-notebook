# Design notebook for week ending November 23, 2014

## Description
This week has been mostly around getting a prototype up and running. I got carried away and actually have a preliminary working version of my DSL. I am lacking in documentation, testing, and thorough error handling, which I will focus on next week. I will supply in my note book entry a preliminary documention of the language and steps to use (which will likely get stream lines as I refactor). I also want to add a syntax for comments.

The language is called MindSketch. File extension is as `.misk`, as in <b><i>Mi</i></b>nd<i><b>Sk</b></i>etch. Pretty clever, huh?

A [simple example](https://github.com/AlejandroFrias/MindSketch/blob/master/code/simple_example.misk) of a `.misk` file. It's just a series of what I call `Translator Objects`.

```
Basic for loop:

PARSER START
(generate|make)? (for)? loop from $START to $END
PARSER END

CODE START: java
for(int i = ${1:$START}; i < ${2:$END}; i++) {
    $0
}
CODE END

CODE START: python
for x in xrange(${1:$START}, ${2:$END}):
    $0
CODE END

Print:

PARSER START
(print|say) $MESSAGE (to)? (the)? (console|screen)?
PARSER END

CODE START: java
System.out.println(${1:"$MESSAGE"});
$0
CODE END

CODE START: python
print(${1:"$MESSAGE"})
$0
CODE END
```

Here there are two Translator Objects, `Basic for loop` and `Print`.

[create_plugin.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/create_plugin.py) is used to generate the Sublime Text 3 plugin. **Note:** I switched to Sublime Text 3 to get access to python3. It is currently in beta, so we'll see if that has any effects on my code later...

```
usage: create_plugin.py [-h] file output

Creates a Sublime Text 3 plugin from the given .misk file.

positional arguments:
  file        .misk file of Translator Objects
  output      file name to write to (inlude the file extension .py)

optional arguments:
  -h, --help  show this help message and exit
```

**Note:**  The file [plugin_template.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/plugin_template.py) must be in the same folder as [create_plugin.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/create_plugin.py)

Running this command on the `.misk` file generates [output.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/output.py).

In Sublime Text 3, `Tools -> New Plugin...`. Copy paste the output and save the file. Check for any syntax errors in the sublime console after saving (open with `ctrl+~`).

The go to `Sublime Text -> Preferences -> Key Bindings - User` and add a key binding for `"command": "prompt_mind_sketch"`. On OSX my key bindings look like this:

```
[
	{ "keys": ["super+shift+m"], "command": "prompt_mind_sketch" }
]
```

Then use away. There are some hidden features by using sublime's snippet language that allows `Tab` to go to user defined fields of a snippet. Play around. The simple one shown only has the two commands, but [mind_sketch3.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/mind_sketch3.py) has a few more.


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I have some features that I want to add, like imports between `.misk` files, commands that only move the cursor, and a web service front end, but I need to focus on documentation, testing and error messages.

Right now, certain typos don't give the best error messages. I have a couple of ways to solve that, but I need to reorganize my code.

If you get a chance, try running the [create_plugin.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/create_plugin.py) on a `.misk` file with typos and give me some feedback on the kinds of errors you would expect vs the ones you're getting.

One biggish implementation issue is that the order that Translator Objects are declared, and the then subsequently made, can have an affect on the plugin. If a Parser Object of one of the Translator Objects captures everything a Parser Object of a different Translator Object, then that other one will never be invoked, which can cause some weirdness. In [mind_sketch3.py](https://github.com/AlejandroFrias/MindSketch/blob/master/code/mind_sketch3.py) try switching the order of declaration so that the `Basic for loop` is added first. Then when inputting the command `loop form 1 to 4 increment by 2`, the `For loop with increment` isn't used and `4 increment by 2` is bound to `$END` instead. Whoops.


**What questions do you have for your critique partners? How can they best help
you?**

~~An issue I have with my DSL right now is the readablilty of the `.misk` file syntax and the subsequently created `output.py` file. If I feel adventurous, I might create a syntax coloring Sublime Text 3 file to make it easier to parse. I think adding comments to the `.misk` that can transfer over to the plugin that is created might also make this nicer. If you have any syntax ideas to make it easier to understand (and still somehow parsable) I'm all ears. I think the web service front end would remove all these problems.~~

Scratch that, I added syntax highlighting. Turned out to be easier than expected. Just save the MindSketch.tmLanguage file to `Packages / User` where you save your plugins and save it.

~~I'm thinking of allowing for multiple Parser Objects per Translator object, to make it easier to have many ways of saying the same thing. Implemenation-wise, I would have done it already if I didn't have other work to do this weekend. But then I though about it. Does it make sense as a feature?~~

Also scratch that. I allow for the declaration of multiple Parser Objects now, or none. You can split up the declaration of Parser Objects and Code Snippets for a particular Trnaslator object as you see fit. I'm getting it ready to allow imports.

I still could use some feed back on error messages. I'm pretty sure those can still suck. At least there are some nice warnings if you forget to declare a Parser Object before your first Code Snippet and an error for when you don't use the same variables between parser objects.

I guess overall comments. I've added a lot. So if there is any process that could use simplification in your eyes, that feedback is welcome. I want it to be usable by programmers for creating a plugins that make coding more accessible for non-programmers. A sort of collaboritive project. If you can't use the language, I need to know why and how to make it easier.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

Oh god, I lost track. As I mentioned before, I got a little carried away. Too much fun!
If I had to guess, I'd say ~~20ish~~ 25ish?

## Post-critique summary

From the critique and discussion in class, there was a general confusion as to the details of the project and architecture. Rightfully so since I was still deep in the research phase. 

## Post-critique reflection
In response, I've added a [grammar](https://github.com/AlejandroFrias/MindSketch/blob/master/documents/grammar.md) to the [documents folder](https://github.com/AlejandroFrias/MindSketch/tree/master/documents). Also I have a working [parser](https://github.com/AlejandroFrias/MindSketch/blob/master/code/pypeg_parser.py) in `pypeg`.

pyPEG2 has been really cool. It allowed me to create the parser and syntax tree at the same time let me use regex's which worked out nicely for me.

```python
class Variable(str):
	grammar = variable

class Word(str):
	grammar = lower_case_word

class Group(str):
	grammar = simple_group
	

class ParserDefine(List):
	grammar = "PARSER START", endl, \
	          some([Word, Variable, Group]), endl, \
	          "PARSER END", endl

class Language(str):
	grammar = language

class CodeSnippet(str):
	grammar = "CODE START", ":", attr("language", Language), endl, \
			  code_snippet, endl,  \
			  "CODE END"

class TranslatorObject(List):
	grammar = name(), ":", endl, \
			  attr("parsers", maybe_some(ParserDefine)), endl, \
			  attr("code_snippets", maybe_some(CodeSnippet))

class MindSketch(List):
	grammar = some(TranslatorObject)
```
Pretty cool right?
