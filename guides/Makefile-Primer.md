# Makefile Primer

## Table of Contents

- [Makefile Primer](#makefile-primer)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Make](#make)
  - [Makefiles](#makefiles)
    - [Structure](#structure)
    - [Variables](#variables)
    - [Targets](#targets)
    - [Commands](#commands)
  - [Using Someone Else's Makefile](#using-someone-elses-makefile)
  - [Writing Your Own Makefile](#writing-your-own-makefile)
  - [Conclusion](#conclusion)

## Introduction

This primer will get you up to speed on what the program `make` and makefiles are, and what they are used for. It will not be an in-depth usage guide, nor a complete documentation, nor an exhaustive list of features. It is only a basic introduction to their usage, primarily written for use in the CS-120 and CS-170 courses. This document will apply to other uses, but its scope is limited intentionally. With that said, let's get see what all the fuss is about.

## Make

`make` is a program. It runs when you run the command `make`. It expects something called a makefile (explained later) to be in the current working directory, named `Makefile`.

In the use case I'm addressing, which is compiling, running, and testing relatively simple C and C++ programs (only a few source files at the most), here's what `make` does when you run it with a makefile: it runs other commands. That's it. It runs commands that you could just run yourself. The benefit of using make, however, is that it can run complex commands, while you only have to type `make`. It can also run different sets of commands, and modify those commands, by simply passing the name of a "target" (also explained later) as a command argument. Doing that looks like this: `make [targetName]` (e.g. `make compile` or `make test1`).

## Makefiles

Makefiles are text files. They contain variables, targets, and commands, stored as text. They are where `make` gets its behavior from. The makefile is what tells `make` what to do when you run it, and it's also where you write the commands you want `make` to execute for each target.

### Structure

Makefiles are divided into sections. There is the top of the file, where global variables are declared, and there are targets below that. A target is a name or set of names (separated by spaces) followed by a colon (`:`). In more advanced applications, there are prerequisites listed after the colon, but for our uses you can ignore that feature. On the lines following the target name(s), the commands to run for that target are listed. Each command you want to have executed must be indented with a tab character (not spaces). A following line which is not indented and has a colon after a name, will be recognized as the next target.

An example makefile, to give you an idea of the structure:

```makefile
VARIABLE=some text that I'd like to replace the name of this variable
COMPILECOMMAND=gcc
COMPILEARGUMENTS=-O -Wextra -Werror -Wall -ansi -pedantic
EXECUTABLENAME=prg.exe

compile:
 $(COMPILECOMMAND) -o $(EXECUTABLENAME) sourcefile.c $(COMPILEARGUMENTS)

1 2:
 ./$(EXECUTABLENAME) $@

memtest:
 valgrind ./$(EXECUTABLENAME) 1
```

Okay, that has  little bit more than I've covered so far, but it will all be explained.

### Variables

Variables in a makefile are used to store long pieces of text that you want to have in multiple different places. In the way we use them here, they're a bit like using `#define` in C/C++. Variable declarations look like this: `VARIABLENAME=variable value` and should each be on their own line. Using a variable is done by writing `$(VARIABLENAME)` somewhere else. For example, in a command. This means that `$(VARIABLENAME)` in the command will be replaced by `variable value`. As you can see in the example above, some uses for variables include compiler argument lists and executable names.

### Targets

Targets are the names you put after `make` to tell `make` what you want it to do. If you don't specify a target name when running `make`, it will default to the first target in the makefile. As mentioned earlier, targets are of the form `targetName:`. When you tell `make` to use a target, it will execute all commands on the lines following that target, until it gets to the next target in the file. Targets are followed by a list of commands, with each line indented with a tab character.

If you want a target to run with slight variation, but pretty much the same behavior as another, you may find it useful to have multiple names for the same target. This is most obvious in the case of having multiple different tests to run, where each test is specified by passing a different value to your executable. If you want this, place each target name on the same line, separated by spaces, and a colon at the end (like a normal target). Now you can use the name of the target in your command with `$@`. This will be replaced with whichever name you call. In the example above, the target `1 2:` can be run with either `make 1` or `make 2`. If I call `make 2`, then `$@` in the command below the target name will be replaced with `2`, making the command `./prg.exe 2`.

### Commands

Here's where make actually *does* things. Commands are executed just like they would be if you ran them yourself on the command line. They are executed in order, from top to bottom. They don't do much special, except that any variables will be resolved to their values before the command actually runs.

---

## Using Someone Else's Makefile

Say, for example, someone else on your team alreay wrote a makefile for your project. Or say, for example, your professor included a makefile with your assignment. Using their makefile is simple.

Look at the contents of the makefile and determine what the available targets are. Again, these are lines that have one or more names followed by a colon. Each name should be descriptive, but you can always check to see what commands are listed under each target. Then, you can run the command `make [target]` to execute a specific target, or just `make` to execute whatever the first target in the file is. If you want/need to edit someone else's makefile, you should know how to write your own makefile first.

## Writing Your Own Makefile

Say, for example, no one gave you a makefile. Making your own makefile is simple.

Are there commands you have to run every time you compile your project? Are there commands you have to run every time you run and test your program? Group each of these into a target. If you have multiple tests that are run with command-line arguments passed to your program, you can make use of the multiple-name feature of target names. Make your target names descriptive of their purpose, but short. Remember, the point of `make` is to require less typing in the future.

Are there parts of commands that are shared between multiple different commands (such as executable names, flag lists, etc.)? Put those into variables so they can be easily modified later.

Constructing a makefile is easiest if you first identify the commands required to build and test your project.

## Conclusion

You should now have some introductory knowledge of how to write and use `make` and makefiles effectively. If you feel there is anything this document did not cover that you think it should, or anything you're left wondering after reading, or anything I can improve, please let me know! My goal is for this document to be easily read and comprehended, and to give you all the knowledge you need to be a more effective developer.

---
Go back to [[index]]
Created: 2022-02-11
Last Updated: 2022-11-09
© 2022 Ian Elsbree

[index]: ../../index "Home Page"
