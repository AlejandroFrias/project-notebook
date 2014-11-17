# Design notebook for week ending November 16, 2014

## Description

**TODO:** Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

I'm on Windows 7, and can't install pypeg2 or anything else with pip for some reason. I edited the system variables correctly, but I still can't even run python from the command prompt.

I may be able to simple use pythons string and re modules, that supply regular expressions that can pull out variables and the formatter to create the generated code I want. So my DSL will target python directly and not some 3rd party library like pyPEG.

```
>>> r = re.compile("generate for( loop)? from (?P<start>.*) to (?P<end>.*)")
>>> m = r.match("generate for loop from 1 to 10")
>>> m.group('start')
'1'
>>> m.group('end')
'10'
>>> template = """for (int i = {0}; i <= {1}; i++) {{

}}"""
>>> print s.format('1', '10')
for (int i = 1; i <= 10; i++) {

}
```

So I think there are enough capabilities here. The trick will be making a language that translates well into this. I think if I stick to something easy to read that has a similar stucture to regex, it should fine.

I think I can use a list of regex's and try to match each one. This would be the implemntation behind the Parser Objects. Priority will be difficult and catching redundant Parser Objects will be difficult, especially when you can import others and are given a few basic ones. Extra care will need to be made with ANY (.*).


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I think I've figured out where to go on the implementation now. This will guide the language a lot. Now I'm writing a lnaguage that will become a Sublime plugin, written in python. Running the a program in my DSL which consists of user made Parser Objects or Translations (name to be decided soon) will translate it into regular expressions to "parse" and string formatting templates to generate code. It will also translate the easy to use cursor placement methods provided into sublime plugin code.

I think this will work out. Right now I need to think of a good intermediate representation that is clean and organized. That's where I am on the design front. I have a good handle now on what constructs and information is needed for creating the sublime plugins.

Also on my to do list is to create a few working sublime plugins for a few of the types of commands I want to support and corressponding AST's that they should be generated from. These will be constantly updated to match my progress as I make more design decisions during implementation.

I also need to decide on a syntax and begin testing how difficult it will be to implement.

**What questions do you have for your critique partners? How can they best help
you?**

I'm still pretty sure I'm doing an external language. From what you've seen, do you agree with me? I know I won't do an internal language within the sublime plugin file (so in python). I like the external language because it will generate a useful intermediate representation. It is theoretically possible that instead of generating a sublime plugin, it generates an eclipse plugin by changing the semantics.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

During the week: At least 4 hours researching and testing various parsers and figuring out feasibility of sublime plugin.

Weekend: 6 hours, most of it Sunday, designing and documenting my design so far. Also, did further research into Python regex and formatter, finding that they will likely work as a target language.

## Post-critique summary

Last weeks critique pointed out that there were a lot of layers to my DSL and how to use. My critique group wanted some diagrams to show the use and the architecture.

## Post-critique reflection

I created the asked for images. Updates to come as implementation really begins to kick into gear.

