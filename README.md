# Python name2type mapping

In October 2018 on the mailing list python-ideas some developers encouraged me, that the idea of a name2type mapping would be usefull.

## Goal

Source code should be clean. Every character which is not needed for my eyes/brain to understand the code should not be on the screen.

Imagine you work on a Django project. Many methods will have the `request` as first argument. Every django develop knows that I mean [django.http.HttpRequest](https://docs.djangoproject.com/en/4.0/ref/request-response/#httprequest-objects).

So if my eyes and brain just need the string `request` to understand what this variable is, then there should be a way
for the interpreter/compiler to understand this, too.

Since interpreter/compilers are not smart, we need a way to make them understand this "name to type mapping".

 
## Syntax Proposal
 
The name2type mapping is defined in the docstring of a Python file.
 
The general syntax is "name2type:" followed by a comma sperated list of variable names. Then ":", then the type hint.
 
Examples:

```
name2type: my_int, my_number, ....: int
name2type: request*: django.http.HttpRequest
```

If the docstring is in a file called `__init__.py`, then the type hints get specified for all files below this directory (recursively).
 
## Use Case Example

Your code base contains a variable name "request" 100 times, and in 70 times the variable type is an instance of "django.http.HttpRequest" (detected by usual type annotations). If you want to have valid type information of all occurences of "request" in your code, then you need to find a solution for 30 usages. You could annotate the variable in your code 30 times (once per method). Or you could define a name2type mapping in the `__init__.py` file if your code.
 
## Misc
 
* The name2type mapping is just a fall-back. First the IDE does the usual type detection and if no type could be found, then name2type mapping gets used. Except explicitly switched off. But this switch is not part of the spec. 
* Related issue at PyCharm: https://youtrack.jetbrains.com/issue/PY-32490

## Arguments against name2type mapping

* It is not needed since stats are enough. Example: If you code base contains a variable name "request" 100 times, and in 70 times the variable type is an instance of "django.http.HttpRequest" (detected by usual type-annotation), then it is redundant to specify this explicit in a file. The IDE (or code quality checking tool) could gather this information by looking at the stats.

Above argument makes me unsure what the best solution looks like. Do an explicit name2type mapping, or leave it up to the stats. There are conflicting guidelines. The guidelines "less is more" and "avoid redundancy" on one side, and on the other side "explicit is better than implicit".

## Open questions

* Use docstring or comment to store the name2type mapping. 
* Is "Rough consensus and working code" enough, or do we need an official PEP?
