---
layout: page
title: Testing
subtitle: Exceptions
minutes: 10
---

> ## Learning Objectives {.objectives}
> 
> *   Learner will understand that exceptions are specialized runtime tests
> *   Learner will recognizes scenarios when to use exceptions and what exceptions are available
> *   Learner will recognize when to use exceptions as opposed to assertions

Exceptions are more sophisticated than assertions. They are the standard error 
messaging system in most modern programming languages.  Fundamentally, when an 
error is encountered, an informative exception is 'thrown' or 'raised'.

For example, instead of the assertion in the case before, an exception can be
used.

~~~ {.python}
def mean(num_list):
    if len(num_list) == 0 :
      raise Exception("The algebraic mean of an empty list is undefined. Please provide a list of numbers")
    else :
      return sum(num_list)/len(num_list)
~~~

Once an exception is raised, it will be passed upward in the program scope.
An exception can be used to trigger additional error messages or an alternative
behavior. Rather than immediately halting code
execution, the exception can be 'caught' upstream with a try-except block.
When wrapped in a try-except block, the exception can be intercepted before it reaches global scope and halts execution.

To add information or replace the message before it is passed upstream, the try-catch block can be used to catch-and-reraise the exception:

~~~ {.python}
def mean(num_list):
    try:
        return sum(num_list)/len(num_list)
    except ZeroDivisionError as detail :
        msg = "The algebraic mean of an empty list is undefined. Please provide a list of numbers."
        raise ZeroDivisionError(detail.__str__() + "\n" +  msg)
~~~

Alternatively, the exception can simply be handled intelligently. If an
alternative behavior is preferred, the exception can be disregarded and a
responsive behavior can be implemented like so:

~~~ {.python}
def mean(num_list):
    try:
        return sum(num_list)/len(num_list)
    except ZeroDivisionError :
        return 0
~~~

If a single function might raise more than one type of exception, each can be
caught and handled separately.

~~~ {.python}
def mean(num_list):
    try:
        return sum(num_list)/len(num_list)
    except ZeroDivisionError :
        return 0
    except TypeError as detail :
        msg = "The algebraic mean of an non-numerical list is undefined. Please provide a list of numbers."
        raise TypeError(detail.__str__() + "\n" +  msg)
~~~

> ## What Else Can Go Wrong? {.challenge}
>
> 1. Think of some other type of exception that could be raised by the try 
> block.
> 2. Guard against it by adding an except clause.

> ## Cause All of the Errors {.challenge}
> 
> - Use the mean function in three different ways, so that you cause each
> exceptional case.

Exceptions have the advantage of being simple to include and powerfully helpful
to the user. However, not all behaviors can or should be found with runtime
exceptions. Most behaviors should be validated with unit tests.

> ## Exceptions vs. Assertions {.callout}
>  To resolve any possible confusion on when to use assertions as opposed to exceptions, we would like to make the following points. 
>  
> 1. _Assertions_ can be thought of as your internal checks (as the developer) 
> to make sure that your program is behaving how you would like it to. When you are writing unit tests for your own software, you should use _assertions_ in those tests since the user will likely not see the tests.
>
> 2. _Exceptions_ can be thought of as messages that you would like the actual user of your program to see to let them know that the program behavior is incorrect (e.g. because their input was not correctly formatted) or to trigger alternative program behaviors. Two particular cases where exceptions are useful is when there is a program failure, and when there are special results or cases that need to be handled.
> A helpful mnemonic is that _Exceptions_ are _external_. 

