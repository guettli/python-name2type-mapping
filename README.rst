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
 
 
