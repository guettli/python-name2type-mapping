Python name2type mapping
=========================

In October 2018 on the mailing list python-ideas some developers encouraged me, that the idea of a name2type mapping would be usefull.

Goal:

* Better type-hints in IDEs.
 
This is not the goal:

* Type-hints which get used during run-time.
 
 
Syntax Proposal
===============
 
The name2type mapping is defined in the docstring of a Python file.
 
The general syntax is "name2type:" followed by a comma sperated list of variable names. Then ":", then the type hint.
 
Examples::
 
     """
     name2type: my_int, my_number, ....: int
     name2type: request*: django.http.HttpRequest
     """"
 
If the docstring is in a file called `__init__.py`, then the type hints get specified for all files below this directory (recursively).
 
Use Case Example
================

Your code base contains a variable name "request" 100 times, and in 70 times the variable type is an instance of "django.http.HttpRequest" (detected by usual type annotations). If you want to have valid type information of all occurences of "request" in your code, then you need to find a solution for 30 usages. You could annotate the variable in your code 30 times (once per method). Or you could define a name2type mapping in the __init__.py file if your code.
 
Misc
====
 
* The name2type mapping is just a fall-back. First the IDE does the usual type detection and if no type could be found, then name2type mapping gets used. Except explicitly switched off. But this switch is not part of the spec. 

Arguments against name2type mapping
===================================

* It is not needed since stats are enough. Example: If you code base contains a variable name "request" 100 times, and in 70 times the variable type is an instance of "django.http.HttpRequest" (detected by usual type-annotation), then it is redundant to specify this explicit in a file. The IDE (or code quality checking tool) could gather this information by looking at the stats.
