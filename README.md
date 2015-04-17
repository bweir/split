
# slit - *a sequential lit tool*

## About

slit is a literate programming tool that places tutorial creation front and center. Now you can write tutorials that will generate examples that your students can run, but explain every single step along the way.

slit is made possible by the magic of literate programming, where code and documentation are intermingled into a single meta-form, from which both code and documentation can be generated.

However, literate programming traditionally emphasizes understanding the program in its current form: as a finished product.

slit doesn't work that way. slit doesn't just tell the story of how the program works; it tells the story of how the program came to be, by providing a much richer way to express the *history* of a program than traditional tools do.

In doing so, slit turns conventional literate programming into an unstoppable tool for creating compelling, provably accurate and up-to-date software tutorials.

### Features

Here are just some of the unusual features of slit

* Total control of code and documentation structure

* Carefully document every single step, including wrong turns, backtracking, and revising code

* Include external files in your tutorial, even other slit files

* Generate **working**, complex, multi-file, multi-language program examples from a single tutorial

* Include the output of shell commands into your documentation

### Who uses slit?

* slit is at the core of the [LameStation programming tutorials](http://www.lamestation.com/learn/demos/latest/03_maps/01_DrawingMaps.spin.html) (in development).

* The README you are reading right now is generated with `./slit -ds README.lit`.

## Installing

`slit` is a single python script and has been tested with Python 2.7.

## Usage

While trying to keep new syntax to a minimum, slit adds some extremely useful features that are hard to find.

### Basics

slit uses markdown for its documentation format, but works with any programming language.

slit files should be marked with with `.lit` extension, appended to the regular file extension.

    hello_world.c.lit

slit works by allow you to assemble code into separate containers, then building your document from them.

Code containers are marked with the `<< blockname >>=` syntax on a line by itself. They must be indented to be accepted as code macros.

    Here is our hello world example!

        << main >=
        int main (void)
        {
            printf("hello world!\n");
        }

The code block will end when the indent level returns to 0.

            printf("hello world!\n");
        }

    The code block is over!

### Basic macros

There are three core elements that make up slit syntax.

* Macro assignment - `<< NAME >>=`

* Macro append - `<< NAME >>+=`

* Macro value - `<< NAME >>`

#### append macro

The append macro (`<< NAME >>+=`) allows you to add code to the end of a new or existing container, where `NAME` is the container name.

#### assignment macro

The assignment macro (`<< NAME >>=`) will add code to a new or existing container, overwriting what was already in it, where `NAME` is the container name.

#### container names

Contain names can be one of the following

* Named containers, containing alphanumeric characters and underscores, like `codeblock1`, `main_function`.

* File containers, containing a single-word filename with extension, like `filename.txt` (*files with spaces or that reside in a different path are not currently supported*)

* The `*` container, which will create a file named after the top-level slit file with the `.lit` extension removed. So for `hello_world.c.lit`, the `*` container will generate the `hello_world.c` code file.

The top-level documentation file is always generated at the source file name with a `.md` extension, so `hello_world.c.lit` will generate `hello_world.c.md`

### Include directive

Use the `#include` directive to organize a single tutorial into multiple files.

    #include "part1.spin"
    #include "part1.diagram"
    #include "part2.spin"
    #include "part2.diagram"
    #include "gfx_cave.lit"
    #include "conclusion.md"

### Shell code

**WARNING: this WILL allow tutorials to execute code on your system. Use with caution.**

Use the shebang macro (`<<#! command >>`) to dump the output of shell commands into your tutorial.

    test/
    ├── bacon
    ├── chicken
    └── turkey

    0 directories, 3 files

This feature is inherently platform and build environment dependent and will make your tutorial build less portable. Use wisely!

This feature is disabled by default. Enable with `-s`.

### More info

For a complete listing of slit parameters, use `--help`:

    usage: slit [-h] [-c] [-d] [-s] [--build-directory] PATH

    A sequential literate processor.

    positional arguments:
      PATH               path to lit file to process (dir or file)

    optional arguments:
      -h, --help         show this help message and exit
      -c, --code         build final source file
      -d, --doc          build markdown documentation
      -s, --shell        enable shell code execution
      --build-directory  scan directory and build every literate file

## Author

slit is created by Brett Weir, and inspired by Connor Osborne's [lit](https://github.com/cdosborn/lit) tool and Donald Knuth, for coming up with literate programming in the first place.

## Bug Reporting

Please report all bugs to the [slit issue tracker](https://github.com/bweir/slit/issues).

