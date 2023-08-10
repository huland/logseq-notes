## Clean Code
collapsed:: true
	- ### The Boy Scout Rule
		- If we all checked-in our code a little cleaner than when we checked it out, the code simply could not rot.
		- The cleanup doesn’t have to be something big:
			- change one variable name for the better
			- break up one function that’s a little too large
			- eliminate one small bit of duplication
			- clean up one composite if statement
## Meaningful Names
collapsed:: true
	- ### Use Intention-Revealing Names
		- Choosing good names takes time but saves more than it takes.
		- Take care with your names and change them when you fnd better ones.
		- The name of a variable, function, or class, should answer all the big questions. It should tell you why it exists, what it does, and how it is used. If a name requires a comment, then the name does not reveal its intent.
		- #### Example
			- What is the purpose of this code?
			- ```java
			  public List<int[]> getThem() {
			    List<int[]> list1 = new ArrayList<int[]>();
			    for (int[] x : theList)
			        if (x[0] == 4)
			            list1.add(x);
			    return list1;
			  }
			  ```
			- Why is it hard to tell what this code is doing?
				- There are no complex expressions.
				- Spacing and indentation are reasonable.
				- There are only three variables and two constants mentioned.
				- There aren’t even any fancy classes or polymorphic methods, just a list of arrays (or so it seems).
			- The problem isn’t the simplicity of the code but the implicity of the code (to coin a phrase): the degree to which the context is not explicit in the code itself.
			- The code implicitly requires that we know the answers to questions such as:
				- 1. What kinds of things are in theList?
				- 2. What is the signifcance of the zeroth subscript of an item in theList?
				- 3. What is the signifcance of the value 4?
				- 4. How would I use the list being returned?
			- The answers to these questions are not present in the code sample, but they could have been.
				- Say that we’re working in a mine sweeper game. We find that the board is a list of cells called theList. Let’s rename that to gameBoard.
				- Each cell on the board is represented by a simple array. We further find that the zeroth subscript is the location of a status value and that a status value of 4 means “flagged.”
				- Just by giving these concepts names we can improve the code considerably:
				- ```java
				  public List<int[]> getFlaggedCells() {
				    List<int[]> flaggedCells = new ArrayList<int[]>();
				    for (int[] cell : gameBoard)
				        if (cell[STATUS_VALUE] == FLAGGED)
				            flaggedCells.add(cell);
				    return flaggedCells;
				  }
				  ```
				- Notice that the simplicity of the code has not changed. It still has exactly the same number of operators and constants, with exactly the same number of nesting levels. But the code has become much more explicit.
	- ### Beware of using names which vary in small ways
		- Spelling similar concepts similarly is information. Using inconsistent spellings is disinformation
			- XYZControllerForEfficientHandlingOfStrings
			- XYZControllerForEfficientStorageOfStrings
	- ### Use Pronounceable Names
		- This matters because programming is a social activity.
	- ### Use Searchable Names
		- Single-letter names and numeric constants have a particular problem in that they are not easy to locate across a body of text.
		- One might easily grep for MAX_CLASSES_PER_STUDENT, but the number 7 could be more
		  troublesome
	- ### Avoid Encodings
		- Encoding type or scope information into names simply adds an extra burden of deciphering.
	- ### Class Names
		- Classes and objects should have noun or noun phrase names like Customer, WikiPage, Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name of a class. A class name should not be a verb.
	- ### Method Names
		- Methods should have verb or verb phrase names like postPayment, deletePage, or save. Accessors, mutators, and predicates should be named for their value and prefxed with get, set, and is according to the javabean standard.
	- ### Avoid Mental Mapping
		- Readers shouldn’t have to mentally translate your names into other names they already know. This problem generally arises from a choice to use neither problem domain terms nor solution domain terms.
		- This is a problem with single-letter variable names
			- There can be no worse reason for using the name `c` than because `a` and `b` were already taken.
		- One difference between a smart programmer and a professional programmer is that the professional understands that clarity is king. Professionals use their powers for good and write code that others can understand.
	- ### Don’t Be Cute
		- If names are too clever, they will be memorable only to people who share the author’s sense of humor, and only as long as these people remember the joke. Will they know what the function named HolyHandGrenade is supposed to do? Sure, it’s cute, but maybe in this case DeleteItems might be a better name.
			- Choose clarity over entertainment value.
			- Say what you mean. Mean what you say
	- ### Pick One Word per Concept
		- It’s confusing to have fetch, retrieve, and get as equivalent methods of different classes.
		- The function names have to stand alone, and they have to be consistent in order for you to pick the correct method without any additional exploration.
		- A consistent lexicon is a great boon to the programmers who must use your code.
	- ### Don’t Pun
		- Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.
		- Our goal, as authors, is to make our code as easy as possible to understand. We want our code to be a quick skim, not an intense study.
	- ### Use Solution Domain Names
		- Go ahead and use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth. It is not wise to draw every name from the problem domain because we don’t want our coworkers to have to run back and forth to the customer asking what every name means when they already know the concept by a different name.
	- ### Use Problem Domain Names
		- Separating solution and problem domain concepts is part of the job of a good programmer and designer.
	- ### Add Meaningful Context
		- You need to place names in context for your reader by enclosing them in well-named classes, functions, or namespaces.
	- ### Don’t Add Gratuitous Context
		- In an imaginary application called “Gas Station Deluxe,” it is a bad idea to prefx every class with GSD.
		- The names `accountAddress` and `customerAddress` are fine names for instances of the class `Address` but could be poor names for classes.
		- `Address` is a fine name for a class.
		- If I need to differentiate between MAC addresses, port addresses, and Web addresses, I might consider `PostalAddress`, `MAC`, and `URI`.
		  The resulting names are more precise, which is the point of all naming.
	- ### Final Words
		- Follow some of these rules and see whether you don’t improve the readability of your code. If you are maintaining someone else’s code, use refactoring tools to help resolve these problems. It will pay off in the short term and continue to pay in the long run.
## Functions
collapsed:: true
	- ### Small
		- The first rule of functions is that they should be small.
		- The second rule of functions is that they should be smaller than that.
			- Every function just two, or three, or four lines long.
			- Each was transparently obvious.
			- Each told a story.
			- And each led you to the next in a compelling order.
			- That’s how short your functions should be!
		- #### Blocks and Indenting
			- This implies that the blocks within if statements, else statements, while statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within the block can have a nicely descriptive name.
			- The indent level of a function should not be greater than one or two, this makes the functions easier to read and understand.
	- ### Do One Thing
		- **FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.**
		- The problem with this statement is that it is hard to know what "one thing" is.
		- If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing. After all, the reason we write functions is to decompose a larger concept (in other words, the name of the function) into a set of steps at the next level of abstraction
		- So, another way to know that a function is doing more than "one thing" is if you can extract another function from it with a name that is not merely a restatement of its implementation.
		- #### Sections within Functions
			- If a function is divided into sections such as
				- declarations
				- initializations
				- sieve
			- That is an obvious symptom of doing more than one thing.
			- Functions that do one thing cannot be reasonably divided into sections.
	- ### One Level of Abstraction per Function
		- #### Reading Code from Top to Bottom: The Stepdown Rule (The Stepdown Rule)
			- We want the code to read like a top-down narrative.
			  We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions.
			- To say this differently, we want to be able to read the program as though it were a set of `TO paragraphs`, each of which is describing the current level of abstraction and referencing subsequent `TO` paragraphs at the next level down.
				- To include the setups and teardowns, we include setups, then we include the test page content, and then we include the teardowns.
					- To include the setups, we include the suite setup if this is a suite, then we include the regular setup.
					- To include the suite setup, we search the parent hierarchy for the "SuiteSetUp" page and add an include statement with the path of that page.
					- To search the parent ...
			- It turns out to be very diffcult for programmers to learn to follow this rule and write functions that stay at a single level of abstraction. But learning this trick is also very important. It is the key to keeping functions short and making sure they do "one thing".
	- ### Switch Statements
		- By their nature, switch statements always do N things.
		- Unfortunately we can’t always avoid switch statements, but we can make sure that each switch statement is buried in a low-level class and is never repeated.
	- ### Use Descriptive Names
		- Describe what the function does.
		- "You know you are working on clean code when each routine turns out to be pretty much what you expected."
			- Half the battle to achieving that principle is choosing good names for small functions that do one thing.
		- The smaller and more focused a function is, the easier it is to choose a descriptive name.
		- Don’t be afraid to make a name long.
			- A long descriptive name is better than a short enigmatic name.
			- A long descriptive name is better than a long descriptive comment.
			- Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.
		- Don’t be afraid to spend time choosing a name.
			- try several different names and read the code with each in place (modern IDEs make it trivial to change names)
		- Choosing descriptive names will clarify the design of the module in your mind and help you to improve it. It is not at all uncommon that hunting for a good name results in a favorable restructuring of the code.
		- Be consistent in your names. Use the same phrases, nouns, and verbs in the function names you choose for your modules.
	- ### Function Arguments
		- The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justifcation—and then shouldn’t be used anyway.
		- Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial. If there’s one argument, it’s not too hard. With two arguments the problem gets a bit more challenging. With more than two arguments, testing every combination of appropriate values can be daunting.
		- Output arguments are harder to understand than input arguments. When we read a function, we are used to the idea of information going in to the function through arguments and out through the return value. We don’t usually expect information to be going out through the arguments. So output arguments often cause us to do a double-take.
		- #### Common Monadic Forms
			- There are two very common reasons to pass a single argument into a function:
				- question about that argument
				- operating on that argument, transforming it into something else and returning
		- A somewhat less common, but still very useful form for a single argument function, is an event (in this form there is an input argument but no output argument).
		- #### Flag Arguments
			- flag arguments are ugly
			- loudly proclaiming that this function does more than one thing
	- ### Have No Side Effects
		- Side effects are lies.
		- Your function promises to do one thing, but it also does other hidden things.
			- Sometimes it will make unexpected changes to the variables of its own class.
			- Sometimes it will make them to the parameters passed into the function or to system globals.
		- In either case they are devious and damaging mistruths that often result in strange temporal couplings and order dependencies.
		- ```java
		  public class UserValidator {
		    private Cryptographer cryptographer;
		        public boolean checkPassword(String userName, String password) {
		        User user = UserGateway.findByName(userName);
		        if (user != User.NULL) {
		            String codedPhrase = user.getPhraseEncodedByPassword();
		            String phrase = cryptographer.decrypt(codedPhrase, password);
		            if ("Valid Password".equals(phrase)) {
		                Session.initialize();
		                return true;
		            }
		        }
		        return false;
		    }
		  }
		  ```
			- The side effect is the call to Session.initialize(), of course.
			- The `checkPassword` function, by its name, says that it checks the password.
			- The name does not imply that it initializes the session.
			- So a caller who believes what the name of the function says runs the risk of erasing the existing session data when he or she decides to check the validity of the user.
		- This side effect creates a temporal coupling.
			- That is, `checkPassword` can only be called at certain times (in other words, when it is safe to initialize the session). If it is called out of order, session data may be inadvertently lost.
		- Temporal couplings are confusing, especially when hidden as a side effect.
			- If you must have a temporal coupling, you should make it clear in the name of the function. In this case we might rename the function `checkPasswordAndInitializeSession`, though that certainly violates **"Do onething."**
		- #### Output Arguments
			- Arguments are most naturally interpreted as inputs to a function.
			- Anything that forces you to check the function signature is equivalent to a double-take. It’s a cognitive break and should be avoided.
	- ### Command Query Separation
		- Functions should either do something or answer something, but not both.
		- Doing both often leads to confusion
		- Consider, for example, the following function:
			- ```java
			  public boolean set(String attribute, String value);
			  ```
		- This function sets the `value` of a named `attribute` and returns `true` if it is successful and `false` if no such attribute exists.
		- This leads to odd statements like this:
			- ```java
			  if (set("username", "unclebob")) ...
			  ```
		- Imagine this from the point of view of the reader.
			- What does it mean?
			- Is it asking whether the "username" attribute was previously set to "unclebob"?
			- Or is it asking whether the "username" attribute was successfully set to "unclebob"?
			- It’s hard to infer the meaning from the call because it’s not clear whether the word "set" is a verb or an adjective.
- ## Comments
  collapsed:: true
	- The proper use of comments is to compensate for our failure to express ourself in code
	- Every time you express yourself in code, you should pat yourself on the back.
	- Every time you write a comment, you should grimace and feel the failure of your ability of expression.
	- Why am I so down on comments? Because they lie. Not always, and not intentionally, but too often. The older a comment is, and the farther away it is from the code it describes, the more likely it is to be just plain wrong. The reason is simple. Programmers can’t realistically maintain them.
	- Too often the comments get separated from the code they describe and become orphaned blurbs of everdecreasing accuracy.
	- Truth can only be found in one place: the code. Only the code can truly tell you what it does. It is the only source of truly accurate information. Therefore, though comments are sometimes necessary, we will expend signifcant energy to minimize them.
	- ### Explain Yourself in Code
	- Which would you rather see? This:
		- ```java
		  // Check to see if the employee is eligible for full benefits
		  if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
		  ```
		- Or this?
		- ```java
		  if (employee.isEligibleForFullBenefits())
		  ```
		- It takes only a few seconds of thought to explain most of your intent in code. In many cases it’s simply a matter of creating a function that says the same thing as the comment you want to write.
	- ### Good Comments
		- #### Legal comments
			- Sometimes our corporate coding standards force us to write certain comments for legal reasons.
		- #### Informative comments
			- It is sometimes useful to provide basic information with a comment.
		- #### Explanation of Intent
			- Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision.
		- #### TO-DO comments
			- It is sometimes reasonable to leave “To do” notes in the form of //TODO comments.
	- ### Bad Comments
		- Most comments fall into this category. Usually they are crutches or excuses for poor code or justifications for insufficient decisions, amounting to little more than the programmer talking to himself.
		- #### Mumbling
			- Plopping in a comment just because you feel you should or because the process requires it, is a hack. If you decide to write a comment, then spend the time necessary to make sure it is the best comment you can write.
		- #### Noise Comments
			- ```java
			  /**
			  * Default constructor.
			  */
			  protected AnnualDateRule() {}
			  ```
			- No, really? Or how about this:
			- ```java
			  /** The day of the month. */
			  private int dayOfMonth;
			  ```
			- And then there’s this paragon of redundancy:
			- ```java
			  /**
			  * Returns the day of the month.
			  *
			  * @return the day of the month.
			  */
			  public int getDayOfMonth() {
			    return dayOfMonth;
			  }
			  ```
		- #### Don’t Use a Comment When You Can Use a Function or a Variable
			- Consider the following stretch of code:
			- ```java
			  // does the module from the global list <mod> depend on the
			  // subsystem we are part of?
			  if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
			  ```
			- This could be rephrased without the comment as
			- ```java
			  ArrayList moduleDependees = smodule.getDependSubsystems();
			  String ourSubSystem = subSysMod.getSubSystem();
			  if (moduleDependees.contains(ourSubSystem))
			  ```
		- #### Commented-Out Code
			- Others who see that commented-out code won’t have the courage to delete it. They’ll think it is there for a reason and is too important to delete. So commented-out code gathers like dregs at the bottom of a bad bottle of wine.
			- ```java
			  this.bytePos = writeBytes(pngIdBytes, 0);
			  //hdrPos = bytePos;
			  writeHeader();
			  writeResolution();
			  //dataPos = bytePos;
			  if (writeImageData()) {
			    writeEnd();
			    this.pngBytes = resizeByteArray(this.pngBytes, this.maxPos);
			  }
			  else {
			    this.pngBytes = null;
			  }
			  return this.pngBytes;
			  ```
				- Why are those two lines of code commented?
				- Are they important?
				- Were they left as reminders for some imminent change?
				  Or are they just cruft that someone commented-out years ago and has simply not bothered to clean up.
			- We’ve had good source code control systems for a very long time now. Those systems will remember the code for us. We don’t have to comment it out any more. Just delete the code. We won’t lose it. Promise.
- ## Formatting
  collapsed:: true
	- Code formatting is important. It is too important to ignore and it is too important to treat religiously. Code formatting is about communication, and communication is the professional developer’s first order of business.
	- ### Team Rules
		- A team of developers should agree upon a single formatting style, and then every member of that team should use that style. We want the software to have a consistent style. We don’t want it to appear to have been written by a bunch of disagreeing individuals.
## Objects and Data Structures
collapsed:: true
	- ### Data/Object Anti-Symmetry
		- The difference between objects and data structures:
			- Objects hide their data behind abstractions and expose functions that operate on that data.
			- Data structure expose their data and have no meaningful functions.
		- Notice the complimentary nature of the two definitions. They are virtual opposites.
		- #### Procedural Shape
			- ```java
			  public class Square {
			    public Point topLeft;
			    public double side;
			  }
			  
			  public class Rectangle {
			    public Point topLeft;
			    public double height;
			    public double width;
			  }
			  
			  public class Circle {
			    public Point center;
			    public double radius;
			  }
			  
			  public class Geometry {
			    public final double PI = 3.141592653589793;
			  
			    public double area(Object shape) throws NoSuchShapeException {
			        if (shape instanceof Square) {
			            Square s = (Square)shape;
			            return s.side * s.side;
			        }
			        else if (shape instanceof Rectangle) {
			            Rectangle r = (Rectangle)shape;
			            return r.height * r.width;
			        }
			        else if (shape instanceof Circle) {
			            Circle c = (Circle)shape;
			            return PI * c.radius * c.radius;
			        }
			        throw new NoSuchShapeException();
			    }
			  }
			  ```
			- What would happen if a `perimeter()` function were added to `Geometry`.
			- The **shape** classes would be unaffected! - Any other classes that depended upon the shapes would also be unaffected!
			- On the other hand, if I add a **new** shape, I must change all the functions in Geometry to deal with it.
			- Again, read that over. Notice that the two conditions are diametrically opposed.
		- #### Polymorphic Shapes
			- ```java
			  public class Square implements Shape {
			    private Point topLeft;
			    private double side;
			    public double area() {
			        return side*side;
			    }
			  }
			  
			  public class Rectangle implements Shape {
			    private Point topLeft;
			    private double height;
			    private double width;
			    public double area() {
			        return height * width;
			    }
			  }
			  
			  public class Circle implements Shape {
			    private Point center;
			    private double radius;
			    public final double PI = 3.141592653589793;
			    public double area() {
			        return PI * radius * radius;
			    }
			  }
			  ```
			- The `area()` method is polymorphic. No `Geometry` class is necessary.
			- If I add a new shape, none of the existing functions are affected.
			- If I add a new function all of the shapes must be changed!
			- > Procedural code (code using data structures) makes it easy to add new functions without changing the existing data structures. OO code, on the other hand, makes it easy to add new classes without changing existing functions.
			- The complement is also true:
			- > Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it hard to add new functions because all the classes must change.
			- So, the things that are hard for OO are easy for procedures, and the things that are hard for procedures are easy for OO!
	- ### DTO - Data Transfer Objects
		- DTOs are very useful structures, especially when communicating with databases or parsing messages from sockets, and so on.
		- #### Active Record
			- Unfortunately we often find that developers try to treat these data structures as though they were objects by putting business rule methods in them. This is awkward because it creates a hybrid between a data structure and an object.
			- The solution, of course, is to treat the Active Record as a data structure and to create separate objects that contain the business rules and that hide their internal data (which are probably just instances of the Active Record)
	- ### Conclusion
		- Objects expose behavior and hide data.
		- Hiding implementation is not just a matter of putting a layer of functions between the variables. Hiding implementation is about abstractions! A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.
			- This makes it easy to add new kinds of objects without changing existing behaviors.
			- It also makes it hard to add new behaviors to existing objects.
		- Data structures expose data and have no signifcant behavior.
			- This makes it easy to add new behaviors to existing data structures.
			- It makes it hard to add new data structures to existing functions.
## Error Handling
collapsed:: true
	- ### Use Exceptions Rather Than Return Codes
		- The problem with returning error codes is that they clutter the caller. The caller must
		  check for errors immediately after the call. Unfortunately, it’s easy to forget.
	- ### Provide Context with Exceptions
		- Provide enough context to determine the source and location of an error.
		- Get a stack trace from any exception; however, a stack trace can’t tell you the intent of the operation that failed.
		- If you are logging in your application, pass along enough information to be able to log the error in your catch.
			- Your Highlight on page 140-140 | Added on Sunday, June 18, 2023 8:32:51 PM
	- ### Wrapping third-party APIs is a best practice
		- When you wrap a third-party API, you minimize your dependencies upon it:
			- You can choose to move to a different library in the future without much penalty.
			- Wrapping also makes it easier to mock out third-party calls when you are testing your own code.
	- ### Don’t Return Null
		- Every other line was a check for null.
		- When we return null, we are essentially creating work for ourselves and foisting problems upon our callers. All it takes is one missing null check to send an application spinning out of control.
	- ### Don’t Pass Null
		- Returning null from methods is bad, but passing null into methods is worse. Unless you are working with an API which expects you to pass null, you should avoid passing null in your code whenever possible.
	- ### Conclusion
		- Clean code is readable, but it must also be robust.
		- These are not conflicting goals.
		- We can write robust clean code if we see error handling as a separate concern, something that is viewable independently of our main logic.
		- To the degree that we are able to do that, we can reason about it independently, and we can make great strides in the maintainability of our code.
## Boundaries
collapsed:: true
	- ### Exploring and Learning Boundaries
		- It’s not our job to test the third-party code, but it may be in our best interest to write tests for the third-party code we use.
		- Learning the third-party code is hard. Integrating the third-party code is hard too. Doing both at the same time is doubly hard.
		- We could write some tests to explore our understanding of the third-party code, such tests are learning tests.
		- In learning tests we call the third-party API, as we expect to use it in our application. We’re essentially doing controlled experiments that check our understanding of that API. The tests focus on what we want out of the API.
		- Not only are learning tests free, they have a positive return on investment. When there are new releases of the third-party package, we run the learning tests to see whether there are behavioral differences.
		- The learning tests end up costing nothing. We had to learn the API anyway, and writing those tests was an easy and isolated way to get that knowledge.
	- ### Using Code That Does Not Yet Exist
		- We manage third-party boundaries by having very few places in the code that refer to them.
			- We may wrap them
			- We may use an ADAPTER to convert from our perfect interface to the provided interface.
		- Either way our code speaks to us better, promotes internally consistent usage across the boundary, and has fewer maintenance points when the third-party code changes.
## Unit Tests
collapsed:: true
	- ### F.I.R.S.T.
		- Clean tests follow five other rules that form the above acronym:
			- Fast (Tests should be fast)
			- Independent (Tests should not depend on each other)
			- Repeatable (Tests should be repeatable in any environment)
			- Self-Validating (Either they pass or fail)
			- Timely
		- The tests need to be written in a timely fashion. Unit tests should be written just before the production code that makes them pass. If you write tests after the production code, then you may find the production code to be hard to test. You may decide that some production code is too hard to test. You may not design the production code to be testable.
	- ### Conclusion
		- Tests are as important to the health of a project as the production code is. Perhaps they are even more important, because tests preserve and enhance the fexibility, maintainability, and reusability of the production code.
		- If you let the tests rot, then your code will rot too. Keep your tests clean
- ## Classes
  collapsed:: true
	- The Single Responsibility Principle (SRP)
		- States that a class or module should have one, and only one, reason to change.
		- This principle gives us both a defnition of responsibility, and a guidelines for class size.
		- Classes should have one responsibility - one reason to change
		- Trying to identify responsibilities (reasons to change) often helps us recognize and create better abstractions in our code.
		- SRP is one of the more important concept in OO design. It’s also one of the simpler concepts to understand and adhere to. Yet oddly, SRP is often the most abused class design principle.
			- Why?
				- Getting software to work and making software clean are two very different activities
				- The problem is that too many of us think that we are done once the program works.
				- We fail to switch to the other concern of organization and cleanliness. We move on to the next problem rather than going back and breaking the overstuffed classes into decoupled units with single responsibilities.
	- Open-Closed Principle (OCP)
		- Classes should be open for extension but closed for modifcation.
		- Open to allow new functionality via subclassing.
		- Make this change while keeping every other class closed.
		  Isolating from change
			- There are concrete classes, which contain implementation details (code), and abstract classes, which represent concepts only.
	- Dependency Inversion Principle (DIP)
		- In essence, the DIP says that our classes should depend upon abstractions, not on concrete details.
- ## Systems
  collapsed:: true
	- We all know it is best to give responsibilities to the most qualifed persons. We often forget that it is also best to postpone decisions until the last possible moment.
	- It lets us make informed choices with the best possible information.
	- Whether you are designing systems or individual modules, never forget to use the simplest thing that can possibly work.
- ## Emergence
  collapsed:: true
	- A design is “simple” if it follows these rules:
		- Runs all the tests
		- Contains no duplication
		- Expresses the intent of the programmer
		- Minimizes the number of classes and methods The rules are given in order of importance.
	- Simple Design Rule 1: Runs All the Tests
		- A system that is comprehensively tested and passes all of its tests all of the time is a testable system. That’s an obvious statement, but an important one. Systems that aren’t testable aren’t verifable. Arguably, a system that cannot be verifed should never be deployed.
		- Making our systems testable pushes us toward a design where our classes are small and single purpose. It’s just easier to test classes that conform to the SRP.
		- Making sure our system is fully testable helps us create better designs.
		- Tight coupling makes it difficult to write tests.
		- The more tests we write, the more we use principles like DIP and tools like dependency injection, interfaces, and abstraction to minimize coupling.
	- Simple Design Rules 2–4: Refactoring
		- Once we have tests, we are empowered to keep our code and classes clean by incrementally refactoring the code.
		- The fact that we have these tests eliminates the fear that cleaning up the code will break it.
	- No Duplication
		- Eliminate duplication, ensure expressiveness, and minimize the number of classes and methods.
		- Duplication is the primary enemy of a well-designed system.
		- It represents additional work, additional risk, and additional unnecessary complexity.
	- Expressive
		- You can express yourself by choosing good names.
		- Keep your functions and classes small.
		- Using standard nomenclature.
		- Design patterns, for example, are largely about communication and expressiveness
		- Well-written unit tests are also expressive. A primary goal of tests is to act as documentation by example. Someone reading our tests should be able to get a quick understanding of what a class is all about.
		- But the most important way to be expressive is to try. All too often we get our code working and then move on to the next problem without giving sufficient thought to making that code easy for the next person to read.
		- So take a little pride in your workmanship. Spend a little time with each of your functions and classes.
			- choose better names,
			- split large functions into smaller functions,
			- and generally just take care of what you’ve created.
			- Care is a precious resource
	- Minimal Classes and Methods
		- Our goal is to keep our overall system small while we are also keeping our functions and classes small.
		- So, although it’s important to keep class and function count low, it’s more important to have tests, eliminate duplication, and express yourself.
- ## Concurrency
	- ### Understand some basic definitions
		- Bound Resources
			- Resources of a fixed size or number used in a concurrent environment. Examples include database connections and fixed-size read/write buffers.
		- Mutual Exclusion
			- Only one thread can access shared data or a shared resource at a time.
		- Starvation
			- One thread or a group of threads is prohibited from proceeding for an excessively long time or forever. For example, always letting fast-running threads through first could starve out longer running threads if there is no end to the fast-running threads.
		- Deadlock
			- Two or more threads waiting for each other to finish. Each thread has a resource that the other thread requires and neither can finish until it gets the other resource.
		- Livelock
			- Threads in lockstep, each trying to do work but fnding another "in the way." Due to resonance, threads continue trying to make progress but are unable to for an excessively long time - or forever.
	- ### Know Your Execution Models
		- Producer-Consumer
			- One or more consumer threads acquire that work from the queue and complete it.
			- The queue between the producers and consumers is a bound resource.
				- Producers must wait for free space in the queue before writing and consumers must wait until there is something in the queue to consume.
		- Readers-Writers
			-
		- [Dining Philosophers](http://en.wikipedia.org/wiki/Dining_philosophers_problem)
			- Philosophers sitting around a table
			- A fork is placed to the left of each philosopher
			- Big bowl of spaghetti in the center of the table
			- Philosophers can eat with 2 forks only
				- Replace philosophers with threads and forks with resources and this problem is similar to many enterprise applications in which processes compete for resources. Unless carefully designed, systems that compete in this way can experience deadlock, livelock, throughput, and effciency degradation.
	- ### Testing Threaded Code
		- Proving that code is correct is impractical. Testing does not guarantee correctness. However, good testing can minimize risk. This is all true in a single-threaded solution. As soon as there are two or more threads using the same code and working with shared data, things get substantially more complex.
		- Recommendation: Write tests that have the potential to expose problems and then run them frequently, with different programatic confgurations and system confgurations and load. If tests ever fail, track down the failure.
			- Don’t ignore a failure just because the tests pass on a subsequent run.
				- Treat spurious failures as candidate threading issues
				- Get your nonthreaded code working frst
				- Make your threaded code pluggable
				- Make your threaded code tunable
				- Run with more threads than processors
				- Run on different platforms
				- Instrument your code to try and force failures
			- ### Treat Spurious Failures as Candidate Threading Issues
				- Bugs in threaded code might exhibit their symptoms once in a thousand, or a million, executions.
				- Do not ignore system failures as one-offs
			- ### Get Your Nonthreaded Code Working First
				- Do not try to chase down nonthreading bugs and threading bugs at the same time. Make sure your code works outside of threads.
			- ### Make Your Threaded Code Pluggable
				- code can be run in several confgurations
					- One thread, several threads, varied as it executes.
					- Threaded code interacts with something that can be both real or a test double.
					- Execute with test doubles that run quickly, slowly, variable.
					- Confgure tests so they can run for a number of iterations.
				- Make your thread-based code especially pluggable so that you can run it in various confgurations.
			- ### Make Your Threaded Code Tunable
				- Getting the right balance of threads typically requires trial an error. Early on, fnd ways to time the performance of your system under different confgurations.
				- Consider allowing it to change while the system is running. Consider allowing self-tuning based on throughput and system utilization.
			- ### Run with More Threads Than Processors
				- Things happen when the system switches between tasks. To encourage task swapping, run with more threads than processors or cores. The more frequently your tasks swap, the more likely you’ll encounter code that is missing a critical section or causes deadlock.
			- ### Run on Different Platforms
				- Multithreaded code behaves differently in different environments.
				- You should run your tests in every potential deployment environment.
				- Recommendation: Run your threaded code on all target platforms early and often.
			- ### Instrument Your Code to Try and Force Failures
				- There are two options for code instrumentation:
					- Hand-coded
					- Automated
- ## Successive Refinement
	- We have satisfed the Boy Scout Rule. We have left this module a bit cleaner than we found it. Not that it wasn’t clean already. The authors had done an excellent job with it. But no module is immune from improvement, and each of us has the responsibility to leave the code a little better than we found it.
- ## Smells and Heuristics
	- ### Comments
		- C1: Inappropriate Information
			- Change histories
			- In general, meta-data such as authors, lastmodifed-date, SPR number, and so on should not appear in comments. Comments should be reserved for technical notes about the code and design.
		- C2: Obsolete Comment
			- comment that has gotten old, irrelevant, and incorrect is obsolete
		- C3: Redundant Comment
			- A comment is redundant if it describes something that adequately describes itself.
				- For example:
					- ```java
					  i++; // increment i
					  ```
			- Comments should say things that the code cannot say for itself.
		- C4: Poorly Written Comment
			- A comment worth writing is worth writing well. If you are going to write a comment, take the time to make sure it is the best comment you can write. Choose your words carefully.
		- A comment worth writing is worth writing well. If you are going to write a comment, take the time to make sure it is the best comment you can write. Choose your words carefully. Use correct grammar and punctuation. Don’t ramble. Don’t state the obvious. Be brief.
		  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 9:02:59 AM
  
  C4: Poorly Written Comment
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 9:03:03 AM
  
  C5: Commented-Out Code
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 9:03:42 AM
  
  Who knows how old it is? Who knows whether or not it’s meaningful? Yet no one will delete it because everyone assumes someone else needs it or has plans for it.
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 9:04:19 AM
  
  When you see commented-out code, delete it! Don’t worry, the source code control system still remembers it
  <==========>
- Your Highlight on page 318 | Added on Monday, July 3, 2023 9:05:06 AM
  
  Environment
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 9:05:14 AM
  
  E1: Build Requires More Than One Step
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 2:44:08 PM
  
  You should be able to check out the system with one simple command and then issue one other simple command to build it
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 2:44:14 PM
  
  E2: Tests Require More Than One Step
  <==========>
- Your Highlight on page 318-318 | Added on Monday, July 3, 2023 2:44:52 PM
  
  In the best case you can run all the tests by clicking on one button in your IDE. In the worst case you should be able to issue a single simple command in a shell
  <==========>
- Your Highlight on page 319 | Added on Monday, July 3, 2023 2:45:00 PM
  
  Functions
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:45:02 PM
  
  F1: Too Many Arguments
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:45:28 PM
  
  More than three is very questionable and should be avoided with prejudice.
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:45:36 PM
  
  F2: Output Arguments
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:45:42 PM
  
  Output arguments are counterintuitive. Readers expect arguments to be inputs, not outputs
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:46:07 PM
  
  F3: Flag Arguments
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:46:13 PM
  
  Boolean arguments loudly declare that the function does more than one thing
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:46:24 PM
  
  F4: Dead Function
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:46:32 PM
  
  Methods that are never called should be discarded
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:46:39 PM
  
  Don’t be afraid to delete the function
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:46:50 PM
  
  source code control system still remembers it
  <==========>
- Your Highlight on page 319 | Added on Monday, July 3, 2023 2:46:56 PM
  
  General
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:47:16 PM
  
  G1: Multiple Languages in One Source
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:47:20 PM
  
  G1: Multiple Languages in One Source File
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:47:58 PM
  
  The ideal is for a source fle to contain one, and only one, language
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:48:05 PM
  
  G2: Obvious Behavior Is Unimplemented
  <==========>
- Your Highlight on page 319-319 | Added on Monday, July 3, 2023 2:48:35 PM
  
  any function or class should implement the behaviors that another programmer could reasonably expect
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 2:49:26 PM
  
  When an obvious behavior is not implemented, readers and users of the code can no longer depend on their intuition about function names. They lose their trust in the original author and must fall back on reading the details of the code
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 2:49:31 PM
  
  G3: Incorrect Behavior at the Boundaries
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 4:44:43 PM
  
  Look for every boundary condition and write a test for it.
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 4:45:01 PM
  
  G4: Overridden Safeties
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 4:46:56 PM
  
  It is risky to override safeties
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 4:47:04 PM
  
  Turning off failing tests and telling yourself you’ll get them to pass later is as bad as pretending your credit cards are free money.
  <==========>
- Your Highlight on page 320-320 | Added on Monday, July 3, 2023 4:47:15 PM
  
  G5: Duplication
  <==========>
- Your Highlight on page 320-320 | Added on Tuesday, July 4, 2023 8:56:22 AM
  
  Every time you see duplication in the code, it represents a missed opportunity for abstraction
  <==========>
- Your Highlight on page 321-321 | Added on Tuesday, July 4, 2023 8:59:31 AM
  
  most of the design patterns that have appeared in the last ffteen years are simply well-known ways to eliminate duplication
  <==========>
- Your Highlight on page 321-321 | Added on Tuesday, July 4, 2023 8:59:49 AM
  
  G6: Code at Wrong Level of Abstraction
  <==========>
- Your Highlight on page 322-322 | Added on Tuesday, July 4, 2023 9:04:51 AM
  
  G7: Base Classes Depending on Their Derivatives
  <==========>
- Your Highlight on page 322-322 | Added on Tuesday, July 4, 2023 9:07:22 AM
  
  G8: Too Much Information
  <==========>
- Your Highlight on page 322-322 | Added on Tuesday, July 4, 2023 9:08:02 AM
  
  Well-defned modules have very small interfaces that allow you to do a lot with a little. Poorly defned modules have wide and deep interfaces that force you to use many different gestures to get simple things done. A well-defned interface does not offer very many functions to depend upon, so coupling is low. A poorly defned interface provides lots of functions that you must call, so coupling is high
  <==========>
- Your Highlight on page 323-323 | Added on Tuesday, July 4, 2023 9:09:10 AM
  
  keep coupling low by limiting information
  <==========>
- Your Highlight on page 323-323 | Added on Tuesday, July 4, 2023 9:09:17 AM
  
  G9: Dead Code
  <==========>
- Your Highlight on page 323-323 | Added on Tuesday, July 4, 2023 9:10:39 AM
  
  When you fnd dead code, do the right thing. Give it a decent burial. Delete it from the system
  <==========>
- Your Highlight on page 323-323 | Added on Tuesday, July 4, 2023 9:10:45 AM
  
  G10: Vertical Separation
  <==========>
- Your Highlight on page 323-323 | Added on Tuesday, July 4, 2023 9:12:33 AM
  
  G11: Inconsistency
  <==========>
- Your Highlight on page 323-323 | Added on Tuesday, July 4, 2023 9:15:31 AM
  
  you use a variable named response to hold an HttpServletResponse, then use the same variable name consistently in the other functions that use HttpServletResponse objects. If you name a method processVerificationRequest, then use a similar name, such as processDeletionRequest, for the methods that process other kinds of requests
  <==========>
- Your Highlight on page 324-324 | Added on Tuesday, July 4, 2023 9:15:38 AM
  
  G12: Clutter
  <==========>
- Your Highlight on page 324-324 | Added on Tuesday, July 4, 2023 9:17:24 AM
  
  Variables that aren’t used, functions that are never called, comments that add no information, and so forth. All these things are clutter and should be removed. Keep your source fles clean, well organized, and free of clutter.
  <==========>
- Your Highlight on page 324-324 | Added on Tuesday, July 4, 2023 9:17:30 AM
  
  G13: Artifcial Coupling
  <==========>
- Your Highlight on page 324-324 | Added on Tuesday, July 4, 2023 5:47:35 PM
  
  Take the time to fgure out where functions, constants, and variables ought to be declared. Don’t just toss them in the most convenient place at hand and then leave them there.
  <==========>
- Your Highlight on page 324-324 | Added on Tuesday, July 4, 2023 5:48:26 PM
  
  G14: Feature Envy
  <==========>
- Your Highlight on page 324-324 | Added on Tuesday, July 4, 2023 5:50:51 PM
  
  The methods of a class should be interested in the variables and functions of the class they belong to, and not the variables and functions of other classes
  <==========>
- Your Highlight on page 325-325 | Added on Tuesday, July 4, 2023 5:56:50 PM
  
  G15: Selector Arguments
  <==========>
- Your Highlight on page 326-326 | Added on Tuesday, July 4, 2023 6:01:03 PM
  
  They can be enums, integers, or any other type of argument that is used to select the behavior of the function. In general it is better to have many functions than to pass some code into a function to select the behavior
  <==========>
- Your Highlight on page 326-326 | Added on Tuesday, July 4, 2023 6:01:15 PM
  
  G16: Obscured Intent
  <==========>
- Your Highlight on page 326-326 | Added on Tuesday, July 4, 2023 6:02:13 PM
  
  We want code to be as expressive as possible
  <==========>
- Your Highlight on page 326-326 | Added on Tuesday, July 4, 2023 6:02:25 PM
  
  G17: Misplaced Responsibility
  <==========>
- Your Highlight on page 327-327 | Added on Tuesday, July 4, 2023 6:09:47 PM
  
  G18: Inappropriate Static
  <==========>
- Your Highlight on page 327-327 | Added on Tuesday, July 4, 2023 6:11:52 PM
  
  In general you should prefer nonstatic methods to static methods. When in doubt, make the function nonstatic. If you really want a function to be static, make sure that there is no chance that you’ll want it to behave polymorphically
  <==========>
- Your Highlight on page 327-327 | Added on Tuesday, July 4, 2023 6:11:57 PM
  
  G19: Use Explanatory Variables
  <==========>
- Your Highlight on page 327-327 | Added on Wednesday, July 5, 2023 8:52:34 AM
  
  to make a program readable is to break the calculations up into intermediate values that are held in variables with meaningful names
  <==========>
- Your Highlight on page 328-328 | Added on Wednesday, July 5, 2023 8:53:42 AM
  
  G20: Function Names Should Say What They Do
  <==========>
- Your Highlight on page 328-328 | Added on Wednesday, July 5, 2023 8:58:38 AM
  
  If you have to look at the implementation (or documentation) of the function to know what it does, then you should work to fnd a better name or rearrange the functionality so that it can be placed in functions with better names.
  <==========>
- Your Highlight on page 328-328 | Added on Wednesday, July 5, 2023 8:58:45 AM
  
  G21: Understand the Algorithm
  <==========>
- Your Highlight on page 329-329 | Added on Wednesday, July 5, 2023 3:22:08 PM
  
  G22: Make Logical Dependencies Physical
  <==========>
- Your Highlight on page 330-330 | Added on Wednesday, July 5, 2023 3:58:41 PM
  
  G23: Prefer Polymorphism to If/Else or Switch/Case
  <==========>
- Your Highlight on page 330-330 | Added on Wednesday, July 5, 2023 9:18:52 PM
  
  G24: Follow Standard Conventions
  <==========>
- Your Highlight on page 330-330 | Added on Wednesday, July 5, 2023 9:19:33 PM
  
  Every team should follow a coding standard based on common industry norms
  <==========>
- Your Highlight on page 330-330 | Added on Wednesday, July 5, 2023 9:19:39 PM
  
  The team should not need a document to describe these conventions because their code provides the examples
  <==========>
- Your Highlight on page 331-331 | Added on Wednesday, July 5, 2023 9:20:07 PM
  
  G25: Replace Magic Numbers with Named Constants
  <==========>
- Your Highlight on page 331-331 | Added on Wednesday, July 5, 2023 9:20:26 PM
  
  This is probably one of the oldest rules in software development
  <==========>
- Your Highlight on page 331-331 | Added on Wednesday, July 5, 2023 9:20:38 PM
  
  In general it is a bad idea to have raw numbers in your code. You should hide them behind well-named constants
  <==========>
- Your Highlight on page 331-331 | Added on Wednesday, July 5, 2023 9:24:51 PM
  
  The term “Magic Number” does not apply only to numbers. It applies to any token that has a value that is not self-describing
  <==========>
- Your Highlight on page 332-332 | Added on Wednesday, July 5, 2023 9:26:24 PM
  
  G26: Be Precise
  <==========>
- Your Highlight on page 332-332 | Added on Wednesday, July 5, 2023 11:05:02 PM
  
  G27: Structure over Convention
  <==========>
- Your Highlight on page 332-332 | Added on Wednesday, July 5, 2023 11:06:01 PM
  
  G28: Encapsulate Conditionals
  <==========>
- Your Highlight on page 333-333 | Added on Thursday, July 6, 2023 8:56:03 AM
  
  G29: Avoid Negative Conditionals
  <==========>
- Your Highlight on page 333-333 | Added on Thursday, July 6, 2023 8:56:40 AM
  
  Negatives are just a bit harder to understand than positives. So, when possible, conditionals should be expressed as positives
  <==========>
- Your Highlight on page 333-333 | Added on Thursday, July 6, 2023 8:56:48 AM
  
  G30: Functions Should Do One Thing
  <==========>
- Your Highlight on page 333-333 | Added on Thursday, July 6, 2023 8:57:35 AM
  
  It is often tempting to create functions that have multiple sections that perform a series of operations. Functions of this kind do more than one thing, and should be converted into many smaller functions, each of which does one thing
  <==========>
- Your Highlight on page 333-333 | Added on Thursday, July 6, 2023 8:58:47 AM
  
  G31: Hidden Temporal Couplings
  <==========>
- Your Highlight on page 334-334 | Added on Thursday, July 6, 2023 9:01:55 AM
  
  G32: Don’t Be Arbitrary
  <==========>
- Your Highlight on page 334-334 | Added on Thursday, July 6, 2023 9:03:28 AM
  
  Each function produces a result that the next function needs, so there is no reasonable way to call them out of order
  <==========>
- Your Highlight on page 334-334 | Added on Thursday, July 6, 2023 9:03:32 AM
  
  G32: Don’t Be Arbitrary
  <==========>
- Your Highlight on page 334-334 | Added on Thursday, July 6, 2023 9:06:17 AM
  
  . If a structure appears arbitrary, others will feel empowered to change it. If a structure appears consistently throughout the system, others will use it and preserve the convention
  <==========>
- Your Highlight on page 335-335 | Added on Thursday, July 6, 2023 9:06:26 AM
  
  G33: Encapsulate Boundary Conditions
  <==========>
- Your Highlight on page 335-335 | Added on Thursday, July 6, 2023 9:07:56 AM
  
  boundary condition that should be encapsulated within a variable
  <==========>
- Your Highlight on page 335-335 | Added on Thursday, July 6, 2023 9:08:01 AM
  
  G34: Functions Should Descend Only One Level of Abstraction
  <==========>
- Your Highlight on page 335-335 | Added on Thursday, July 6, 2023 9:08:49 AM
  
  The statements within a function should all be written at the same level of abstraction, which should be one level below the operation described by the name of the function. This may be the hardest of these heuristics to interpret and follow
  <==========>
- Your Highlight on page 336-336 | Added on Thursday, July 6, 2023 9:12:59 AM
  
  Separating levels of abstraction is one of the most important functions of refactoring, and it’s one of the hardest to do well
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:14:28 AM
  
  G35: Keep Confgurable Data at High Levels
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:16:37 AM
  
  do not bury it in a low-level function
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:16:47 AM
  
  Expose it as an argument to that low-level function called from the high-level function
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:21:45 AM
  
  The confguration constants reside at a very high level and are easy to change. They get passed down to the rest of the application. The lower levels of the application do not own the values of these constants
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:21:49 AM
  
  G36: Avoid Transitive Navigation
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:22:30 AM
  
  In general we don’t want a single module to know much about its collaborators. More specifcally, if A collaborates with B, and B collaborates with C, we don’t want modules that use A to know about C. (For example, we don’t want a.getB().getC().doSomething()
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 9:23:38 AM
  
  making sure that modules know only about their immediate collaborators and do not know the navigation map of the whole system.
  <==========>
- Your Highlight on page 337-337 | Added on Thursday, July 6, 2023 11:23:35 AM
  
  If many modules used some form of the statement a.getB().getC(), then it would be diffcult to change the design and architecture to interpose a Q between B and C
  <==========>
- Your Highlight on page 338-338 | Added on Thursday, July 6, 2023 11:23:57 AM
  
  This is how architectures become rigid. Too many modules know too much about the architecture
  <==========>
- Your Highlight on page 339-339 | Added on Thursday, July 6, 2023 11:26:37 AM
  
  Constants versus Enums
  <==========>
- Your Highlight on page 339-339 | Added on Thursday, July 6, 2023 11:26:47 AM
  
  Now that enums have been added to the language (Java 5), use them
  <==========>
- Your Highlight on page 339-339 | Added on Thursday, July 6, 2023 11:27:02 AM
  
  The meaning of ints can get lost. The meaning of enums cannot, because they belong to an enumeration that is named
  <==========>
- Your Highlight on page 339-339 | Added on Thursday, July 6, 2023 11:27:26 AM
  
  What’s more, study the syntax for enums carefully. They can have methods and felds. This makes them very powerful tools that allow much more expression and fexibility than ints
  <==========>
- Your Highlight on page 340-340 | Added on Thursday, July 6, 2023 11:28:13 AM
  
  N1: Choose Descriptive Names
  <==========>
- Your Highlight on page 340-340 | Added on Thursday, July 6, 2023 11:28:49 AM
  
  Don’t be too quick to choose a name. Make sure the name is descriptive. Remember that meanings tend to drift as software evolves, so frequently reevaluate the appropriateness of the names you choose
  <==========>
- Your Highlight on page 340-340 | Added on Thursday, July 6, 2023 11:29:01 AM
  
  This is not just a “feel-good” recommendation. Names in software are 90 percent of what make software readable
  <==========>
- Your Highlight on page 341-341 | Added on Thursday, July 6, 2023 12:45:51 PM
  
  “pretty much what you expected.
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 12:46:06 PM
  
  N2: Choose Names at the Appropriate Level of Abstraction
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 12:46:22 PM
  
  Don’t pick names that communicate implementation; choose names the refect the level of abstraction of the class or function you are working in
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 12:47:04 PM
  
  Each time you make a pass over your code, you will likely fnd some variable that is named at too low a level. You should take the opportunity to change those names when you fnd them. Making code readable requires a dedication to continuous improvement
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 12:49:16 PM
  
  N3: Use Standard Nomenclature Where Possible
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 12:49:24 PM
  
  Names are easier to understand if they are based on existing convention or usage
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 12:49:38 PM
  
  Patterns are just one kind of standard
  <==========>
- Your Highlight on page 342-342 | Added on Thursday, July 6, 2023 6:13:52 PM
  
  It is better to follow conventions like these than to invent your own.
  <==========>
- Your Highlight on page 343-343 | Added on Thursday, July 6, 2023 6:15:04 PM
  
  N4: Unambiguous Names
  <==========>
- Your Highlight on page 343-343 | Added on Thursday, July 6, 2023 6:16:19 PM
  
  N5: Use Long Names for Long Scopes
  <==========>
- Your Highlight on page 343-343 | Added on Thursday, July 6, 2023 6:17:50 PM
  
  The length of a name should be related to the length of the scope. You can use very short variable names for tiny scopes, but for big scopes you should use longer names
  <==========>
- Your Highlight on page 343-343 | Added on Thursday, July 6, 2023 6:17:55 PM
  
  name should be. N6
  <==========>
- Your Highlight on page 343-343 | Added on Thursday, July 6, 2023 6:18:01 PM
  
  N6: Avoid Encodings
  <==========>
- Your Highlight on page 343-343 | Added on Thursday, July 6, 2023 6:24:03 PM
  
  Names should not be encoded with type or scope information
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:24:10 PM
  
  N7: Names Should Describe Side-Effects
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:24:56 PM
  
  Names should describe everything that a function, variable, or class is or does
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:25:02 PM
  
  Don’t use a simple verb to describe a function that does more than just that simple action
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:25:27 PM
  
  T1: Insuffcient Tests
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:25:59 PM
  
  ” A test suite should test everything that could possibly break. The tests are insuffcient so long as there are conditions that have not been explored by the tests or calculations that have not been validated
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:26:07 PM
  
  A test suite should test everything that could possibly break. The tests are insuffcient so long as there are conditions that have not been explored by the tests or calculations that have not been validated
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:26:11 PM
  
  T2: Use a Coverage Tool
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:26:33 PM
  
  They make it easy to fnd modules, classes, and functions that are insuffciently tested
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:26:49 PM
  
  T3: Don’t Skip Trivial Tests
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:26:52 PM
  
  T3: Don’t Skip Trivial Tests
  <==========>
- Your Highlight on page 344-344 | Added on Thursday, July 6, 2023 6:27:13 PM
  
  T4: An Ignored Test Is a Question about an Ambiguity
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:28:36 PM
  
  T5: Test Boundary Conditions
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:29:52 PM
  
  Take special care to test boundary conditions
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:30:05 PM
  
  T6: Exhaustively Test Near
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:30:09 PM
  
  T6: Exhaustively Test Near Bugs
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:36:31 PM
  
  T7: Patterns of Failure Are Revealing
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:38:18 PM
  
  T8: Test Coverage Patterns Can Be Revealing
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:38:45 PM
  
  Looking at the code that is or is not executed by the passing tests gives clues to why the failing tests fail
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:38:51 PM
  
  T9: Tests Should Be
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:39:16 PM
  
  T9: Tests Should Be Fast
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:39:46 PM
  
  A slow test is a test that won’t get run. When things get tight, it’s the slow tests that will be dropped from the suite. So do what you must to keep your tests fast
  <==========>
- Your Highlight on page 345-345 | Added on Thursday, July 6, 2023 6:41:35 PM
  
  Conclusion This list of heuristics and smells could hardly be said to be complete. Indeed, I’m not sure that such a list can ever be complete. But perhaps completeness should not be the goal, because what this list does do is imply a value system. Indeed, that value system has been the goal, and the topic, of this book. Clean code is not written by following a set of rules. You don’t become a software craftsman by learning a list of heuristics. Professionalism and craftsmanship come from values that drive disciplines
  <==========>
- Your Highlight on page 372-372 | Added on Thursday, July 13, 2023 5:16:53 PM
  
  Monte Carlo Testing. Make tests fexible, so they can be tuned. Then run the test over and over—say on a test server—randomly changing the tuning values. If the tests ever fail, the code is broken. Make sure to start writing those tests early so a continuous integration server starts running them soon. By the way, make sure you carefully log the conditions under which the test failed
  <==========>
- Your Highlight on page 372-372 | Added on Thursday, July 13, 2023 5:18:20 PM
  
  Run the test on every one of the target deployment platforms.Repeatedly.Continuously. The longer the tests run without failure, the more likely that – The production code is correct or – The tests aren’t adequate to expose problems
  <==========>
- Your Highlight on page 372-372 | Added on Thursday, July 13, 2023 5:18:36 PM
  
  Run the tests on a machine with varying loads. If you can simulate loads close to a production environment
  <==========>
- Your Highlight on page 372-372 | Added on Thursday, July 13, 2023 5:18:46 PM
  
  Run the tests on a machine with varying loads. If you can simulate loads close to a production environment, do so
  <==========>
- Your Highlight on page 373-373 | Added on Thursday, July 13, 2023 5:20:01 PM
  
  Yet, even if you do all of these things, you still don’t stand a very good chance of fnding threading problems with your code. The most insidious problems are the ones that have such a small cross section that they only occur once in a billion opportunities. Such problems are the terror of complex systems
  <==========>
- Your Highlight on page 373-373 | Added on Thursday, July 13, 2023 5:20:33 PM
  
  Tool Support for Testing Thread-Based Code
  <==========>