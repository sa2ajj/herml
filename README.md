## Herml [![Build Status](https://travis-ci.org/tmcgilchrist/herml.png?branch=master)](https://travis-ci.org/tmcgilchrist/herml)
Welcome to herml, the Haml-like templating language!

Building:
* Install leex 0.3 or greater. Putting it in your $ERLANG_HOME/lib is best.
   leex is included with R13B01.
* Clone the herml repo from Github.
* Run make
* Put the herml/ebin directory somewhere on your code path:
  * Symlink the top-level herml directory into your $ERLANG_HOME/lib directory
                                -or-
  * Use the -pz or -pa switches on erl to place herml/ebin onto your code path

Using in Sinan:
* Clone the herml repo from Github
* Run `make special` in the herml directory
* Make sure your sinan project can find the herml repo
   * Clone inside your projects lib directory
                  -or-
   * Symlink the herml directory to your projects lib directory

*  Keep it up to date:
  *  Pull down latest changes
  * `make clean`
  * `make special`

Running tests:

* Run make clean tests


Using herml:

* Start up a herml_manager process for your template directory:

1> herml_manager:start_link(my_web_app,"/path/to/templates").

Note: herml_manager can cache the compiled template and use it over and over.

* Execute the template by calling the herml_manager process:

2> Result = herml_manager:execute_template("file.herml", Env).

Note: Env is a proplist containing the execution environment for the
template. herml expects all variable names to be Erlang strings. For
example, here's a valid environment proplists: [{"UserName", "herml"}].

The UserName variable would be referenced from herml as @UserName.

Another note: For efficiency reasons, herml_manager:execute_template/2,3,4
returns iolists when it executes templates. If you want to view the
template output as a standard string, you can use the io module
to flatten the iolist:

3> io:format("~s", [Result]).
