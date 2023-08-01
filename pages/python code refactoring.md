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
	- 2. Duplicate code
	- 3. Not using available built-in functions
	- 4. Vague identifiers
	- 5. Using isinstance to separate behavior
	- 6. Using boolean flags to make a method do 2 different things
	- 7. Catching and then ignoring exceptions
	- 8. Not using custom exceptions
	- 9. Using the wrong data structure
	- 10. Using misleading names
	- 11. Classes with too many instance variables
	- 12. Verb/subject
	- 13. Backpedalling
	- 14. Hard-wired sequences with a fixed order
	- 15. Creating unrelated objects in the initializer
	- 16. Not relying on keyword arguments
- ## Sources:
	- [Arjan Codes - Python Code Smells](https://www.youtube.com/watch?v=LrtnLEkOwFE)
	- [Arjan Codes - Even More Code Smells](https://www.youtube.com/watch?v=Kl3_Gmn4Ujg)