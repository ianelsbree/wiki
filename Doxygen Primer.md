# Doxygen Primer

By Ian Elsbree, 2022-09-19

-----

## Table of Contents

- [Doxygen Primer](#doxygen-primer)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Doxygen](#doxygen)
  - [Doxygen Comments](#doxygen-comments)
  - [Doxyfiles](#doxyfiles)
    - [Using Someone Else's Doxyfile](#using-someone-elses-doxyfile)
  - [Turning LaTeX into PDF](#turning-latex-into-pdf)
  - [Conclusion](#conclusion)

## Introduction

Welcome to the Doxygen Primer! This document is meant to get you up to speed on Doxygen, a documentation generator that makes it easy to document your code. This primer is not an in-depth usage guide, nor a complete documentation, nor an exhaustive list of features. It is only a basic introduction to the usage of Doxygen, primarily written for use in the CS-120, CS-170, and CS-180 courses. Of course, this document will apply to other uses, but its scope is limited intentionally. With that said, let's see what all the fuss is about.

## Doxygen

Doxygen is a program. It runs when you run the command `doxygen`. It expects something called a doxyfile (explained later) to be in the current working directory, named `Doxyfile`.

Here is the official [Doxygen Manual](https://doxygen.nl/manual/).

Doxygen's purpose is to scan source code files, in this context `.c` or `.cpp` (or `.h`) files, and generate documentation on the code within them, so that other programmers can more easily understand the purpose of your code and how to use it. It does this by generating files in either HTML format or LaTeX format (or both), which you can then use either as an HTML webpage, or use another tool such as `pdf-latex` to generate a PDF file from the LaTeX files. Either of these options will result in a document which explains how your code works to the reader.

Doxygen is not complicated to use in a simple use case. Most basically, you only have to run the command `doxygen -g` to generate a default configuration file, and then run the command `doxygen` to create the documentation for your code. However, there is some more information which will be useful to know about.

## Doxygen Comments

Doxygen scans the comments in your source code. To make Doxygen aware of the information it needs to generate the documentation, you need to use special comments. You will need to put a Doxygen comment at the top of your file (a file header), specifying information about the file, as well as comments above each of your functions (function headers), specifying information about each of them. Here is an example Doxygen-style comment (this one is for a function):

```c
/**
 * @brief Dynamically allocates a new node, initializing it with data.
 *
 * @param value The value to store in the node
 * @param label The label to associate with the node
 * @return A pointer to the newly made node
 */
```

Okay, what do we see here? A few things:

- Doxygen comments begin with an extra `*` symbol, so you get `/**` instead of the normal `/*`.
- The asterisks at the beginning of each line are optional. They just look nice.
- Each line contains what's called a tag, followed by information.
  - Tags start with either a `@` or a `\` (either one works).
  - Tags denote some kind of information that would be useful to have in the documentation of your code.
  - The name of the tag determines how it is used in the documentation.
- The information after the tag is displayed in the documentation.
- Doxygen comments end like normal comments.

The most notable tags you will use are:

- `@file` - Used as the name of the file the code is in.
- `@author` - Used to credit the author of the file.
- `@date` - Used to record the date of authorship of the file, or, in the case of the CS courses I mentioned earlier, the due date of the assignment.
- `@par` - Used to display any information that does not have its own tag. If you use this tag and place a field name, and the field value on the following line, it will be displayed in the same way the `author` and `date` tags are.
- `@brief` - Used to give a short description to a file or a function.
- `@param` - Used to give the parameters of a function. The first word after the tag is the name of the parameter, and everything after that is the description of the parameter.
- `@return` - Used to give the return value of a function.

There are other tags, although they are not as frequent, depending on the type of programming you do. Refer to the official manual for more information.

## Doxyfiles

When you run Doxygen, it looks for a configuration file called a doxyfile. The default name it will look for is `Doxyfile`, with no file extension. A doxyfile is a text file, much in the same way that a C source code file is a text file. If you look at the default doxyfile (generated with the command `doxygen -g`), you can see the structure of a doxyfile, with options, followed by `=`, followed by values.

Notable options include:

- `PROJECT_NAME` - The title of your documentation. Be sure to change this.
- `GENERATE_LATEX` and `GENERATE_HTML` - Select what kind of documentation files to generate.

There are many, many more options available, although these are the most critical. Again, refer to the official manual for more information.

### Using Someone Else's Doxyfile

If someone such as your professor provides a file named `Doxyfile`, good news! You don't have to configure one yourself. However, this is **very** important: make sure you edit the doxyfile to change the `PROJECT_NAME` to something suitable.

Other than that, using someone else's doxyfile is as simple as putting it the directory of your project and running the command `doxygen`. That's it. You should see a new folder or two, depending on what type of documentation you're generating. Inside these folders is your fresh, hot-off-the-press documentation. Have fun!

## Turning LaTeX into PDF

You may have generated LaTeX documentation, but to view that, you'll need a program that can render LaTeX markup. Instead, you can generate a PDF document that more people's computers will be able to display easily.

Inside of the `latex` folder that was generated, you'll see a makefile, intended for the program `make`. Surprise! I have a primer on `make` and makefiles [here](https://gist.github.com/beppyboo/918469df1e90f08b8e4bea4825cc814b). But for this usage, you should only need to run the commands `cd latex` to get into the `latex` directory and `make` to generate a PDF of your documentation. You will need a command called `pdflatex` for the makefile to work properly, which can be gotten as part of a package set called `texlive`.

After you run `make`, you'll see a file called `refman.pdf` is generated. That file is a PDF document that contains the full documentation for your project. Congratulations! Doesn't it look pretty?

## Conclusion

You should now have some introductory knowledge of how to use Doxygen effectively. If you feel there is anything this document did not cover that you think it should, or anything you're left wondering after reading, or anything I can improve, please let me know! My goal is for this document to be easily read and comprehended, and to give you all the knowledge you need to be a more effective developer.

---

By Ian Elsbree, 2022-09-19

ianelsbree@gmail.com

ian.elsbree@digipen.edu

---
Go back to [[index]]
Created: 2022-11-09
Last Updated: 2022-11-09
© 2022 Ian Elsbree
