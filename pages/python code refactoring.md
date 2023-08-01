- Do not use wildcard imports (\*)
	- no control over what is beeing imported
	- later (when you'd refactor) hard to figure out where a particaular object, function, class etc is coming from
- Use guard clauses
	- Guard clasuses:
	- ```python
	  def my_dumy_checker():
	    for my_obj in my_object:
	      if my_obj.dummy == "something":
	        if check_something(my_obj):
	          return False
	        if not check_something_else(my_obj):
	          return False
	      return True
	  ```
	- ```python
	  def my_dumy_checker():
	    for my_obj in my_object:
	      if my_obj.dummy != "something":
	        continue
	      if check_something(my_obj):
	        return False
	      if not check_something_else(my_obj):
	        return False
	      return True
	  ```
- ## Code smells
	- 1. Imprecise types
	- 1. Duplicate code
	- 1. Not using available built-in functions
	- 1. Vague identifiers
	- 1. Using isinstance to separate behavior
	- 1. Using boolean flags to make a method do 2 different things
	- 1. Catching and then ignoring exceptions
	- 1. Not using custom exceptions
	- 1. Using the wrong data structure
	- 1. Using misleading names
	- 1. Classes with too many instance variables
	- 1. Verb/subject
	- 1. Backpedalling
	- 1. Hard-wired sequences with a fixed order
	- 1. Creating unrelated objects in the initializer
	- 1. Not relying on keyword arguments
- sources:
	- [Arjan Codes - Python Code Smells](https://www.youtube.com/watch?v=LrtnLEkOwFE)
	- [Arjan Codes - Even More Code Smells](https://www.youtube.com/watch?v=Kl3_Gmn4Ujg)