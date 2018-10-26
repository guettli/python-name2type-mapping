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
 
 
Misc
====
 
* The name2type mapping is just a fall-back. First the IDE does the usual type detection and if no type could be found, then name2type mapping gets used. Except explicitly switched off. But this switch is not part of the spec. This is up to the IDE how to handle switching name2type on or off.
