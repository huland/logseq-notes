- ## What is Design and Architecture?
	- The measure of design quality is simply the measure of the effort required to meet the needs of the customer. If that effort is low, and stays low throughout the lifetime of the system, the design is good. If that effort grows with each new release, the design is bad. It’s as simple as that.
	- ### Eisenhower's matrix
		- Eisenhower said:
			- I have two kinds of problems, the `urgent` and the `important`. The urgent are not important, and the important are never urgent.
		- The ﬁrst value of software -behavior- is urgent but not always particularly important.
		- The second value of software -architecture- is important but never particularly urgent.
		- We can arrange these four couplets into priorities:
			- `urgent` and `important`
			  logseq.order-list-type:: number
			- `not urgent` and `important`
			  logseq.order-list-type:: number
			- `urgent` and `not important`
			  logseq.order-list-type:: number
			- `not urgent` and `important`
			  logseq.order-list-type:: number
		- Note that the architecture of the code -the important stuﬀ- is in the top two positions of this list, whereas the behavior of the code occupies the ﬁrst and third positions.
	- ### Fight for the Architecture
		- Just remember: If architecture comes last, then the system will become ever more costly to develop, and eventually change will become practically impossible for part or all of the system. If that is allowed to happen, it means the software development team did not fight hard enough for what they knew was necessary.
- ## DESIGN PRINCIPLES
	- The SOLID principles tell us how to arrange our functions and data structures into classes, and how those classes should be interconnected.
		- A class is simply a coupled grouping of functions and data.
	- The goal of the principles is the creation of mid-level software structures that:
		- Tolerate change,
		- Are easy to understand, and
		- Are the basis of components that can be used in many software systems.
	- Executive summary:
		- SRP: The Single Responsibility Principle
			- An active corollary to Conway’s law: The best structure for a software system is heavily influenced by the social structure of the organization that uses it so that each software module has one, and only one, reason to change.
		- OCP: The Open-Closed Principle
			- Bertrand Meyer made this principle famous in the 1980s. The gist is that for software systems to be easy to change, they must be designed to allow the behavior of those systems to be changed by adding new code, rather than changing existing code.
		- LSP: The Liskov Substitution Principle
			- Barbara Liskov’s famous definition of subtypes, from 1988. In short, this principle says that to build software systems from interchangeable parts, those parts must adhere to a contract that allows those parts to be substituted one for another.
		- ISP: The Interface Segregation Principle
			- This principle advises software designers to avoid depending on things that they don’t use.
		- DIP: The Dependency Inversion Principle
			- The code that implements high-level policy should not depend on the code that implements low-level details. Rather, details should depend on policies.
- ## SRP: THE SINGLE RESPONSIBILITY PRINCIPLE
	- the best way to understand this principle is by looking at the symptoms of violating it
		- SYMPTOM 1: ACCIDENTAL DUPLICATION
			- My favorite example is the Employee class from a payroll application. It has three methods: calculatePay(), reportHours(), and save()
			- This class violates the SRP because those three methods are responsible to three very different actors.
			- The calculatePay() method is specified by the accounting department, which reports to the CFO.
			- The reportHours() method is specified and used by the human resources department, which reports to the COO. • The save() method is specified by the database administrators (DBAs), who report to the CTO.
			- By putting the source code for these three methods into a single Employee class, the developers have coupled each of these actors to the others.
			- For example, suppose that the calculatePay() function and the reportHours() function share a common algorithm for calculating non-overtime hours.
			- into a function named regularHours()
			  =-=-=-=-=-=-=-=-=-=
			  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1116-1117 | Added on Monday, August 7, 2023 9:13:26 AM
  
  Now suppose that the CFO’s team decides that the way non-overtime hours are calculated needs to be tweaked. In contrast, the COO’s team in HR does not want that particular tweak because they use non-overtime hours for a different purpose.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1118-1120 | Added on Monday, August 7, 2023 9:13:38 AM
  
  A developer is tasked to make the change, and sees the convenient regularHours() function called by the calculatePay() method. Unfortunately, that developer does not notice that the function is also called by the reportHours() function.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1121-1124 | Added on Monday, August 7, 2023 9:14:06 AM
  
  The developer makes the required change and carefully tests it. The CFO’s team validates that the new function works as desired, and the system is deployed. Of course, the COO’s team doesn’t know that this is happening. The HR personnel continue to use the reports generated by the reportHours() function—but now they contain incorrect numbers.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1125-1127 | Added on Monday, August 7, 2023 5:49:19 PM
  
  We’ve all seen things like this happen. These problems occur because we put code that different actors depend on into close proximity. The SRP says to separate the code that different actors depend on.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1127-1127 | Added on Monday, August 7, 2023 5:49:26 PM
  
  SYMPTOM 2: MERGES
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1132-1133 | Added on Monday, August 7, 2023 5:52:05 PM
  
  Two different developers, possibly from two different teams, check out the Employee class and
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1132-1133 | Added on Monday, August 7, 2023 5:52:15 PM
  
  Two different developers, possibly from two different teams, check out the Employee class and begin to make changes. Unfortunately their changes collide. The result is a merge.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1134-1134 | Added on Monday, August 7, 2023 5:52:31 PM
  
  merges are risky affairs.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1138-1139 | Added on Monday, August 7, 2023 5:53:20 PM
  
  Once again, the way to avoid this problem is to separate code that supports different actors.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1139-1139 | Added on Monday, August 7, 2023 5:53:27 PM
  
  SOLUTIONS
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1141-1144 | Added on Monday, August 7, 2023 5:56:42 PM
  
  separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1141-1146 | Added on Monday, August 7, 2023 5:57:06 PM
  
  separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided. Figure 7.3 The three classes do not know about each other The
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1141-1143 | Added on Monday, August 7, 2023 5:57:23 PM
  
  separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1141-1144 | Added on Monday, August 7, 2023 5:57:32 PM
  
  separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1146-1147 | Added on Monday, August 7, 2023 5:57:47 PM
  
  The downside of this solution is that the developers now have three classes that they have to instantiate and track. A common solution to this dilemma is to use the Facade
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1141-1146 | Added on Monday, August 7, 2023 5:58:01 PM
  
  separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided. Figure 7.3 The three classes do not know about each other The
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1141-1144 | Added on Monday, August 7, 2023 5:58:10 PM
  
  separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1146-1147 | Added on Monday, August 7, 2023 5:58:58 PM
  
  The downside of this solution is that the developers now have three classes that they have to instantiate and track. A common solution to this dilemma is to use the Facade pattern
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1150-1151 | Added on Monday, August 7, 2023 6:00:20 PM
  
  The EmployeeFacade contains very little code. It is responsible for instantiating and delegating to the classes with the functions.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1161-1161 | Added on Monday, August 7, 2023 6:19:35 PM
  
  CONCLUSION
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1162-1164 | Added on Monday, August 7, 2023 6:19:38 PM
  
  The Single Responsibility Principle is about functions and classes—but it reappears in a different form at two more levels. At the level of components, it becomes the Common Closure Principle. At the architectural level, it becomes the Axis of Change responsible for the creation of Architectural Boundaries.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1165-1166 | Added on Monday, August 7, 2023 6:19:44 PM
  
  OCP: THE OPEN-CLOSED PRINCIPLE
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1165-1166 | Added on Monday, August 7, 2023 6:19:48 PM
  
  OCP: THE OPEN-CLOSED PRINCIPLE
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1169-1169 | Added on Monday, August 7, 2023 6:21:12 PM
  
  A software artifact should be open for extension but closed for modification.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1170-1171 | Added on Monday, August 7, 2023 6:21:17 PM
  
  In other words, the behavior of a software artifact ought to be extendible, without having to modify that artifact.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Note on Location 1176 | Added on Monday, August 7, 2023 7:27:24 PM
  
  Make notes with the image when i take notes on this part.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1176-1176 | Added on Monday, August 7, 2023 7:27:24 PM
  
  A THOUGHT EXPERIMENT
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1243-1243 | Added on Tuesday, August 8, 2023 1:16:44 PM
  
  CONCLUSION
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1243-1245 | Added on Tuesday, August 8, 2023 1:16:49 PM
  
  The OCP is one of the driving forces behind the architecture of systems. The goal is to make the system easy to extend without incurring a high impact of change. This goal is accomplished by partitioning the system into components, and arranging those components into a dependency hierarchy that protects higher-level components from changes in lower-level components.
  =-=-=-=-=-=-=-=-=-=
  Clean Architecture: A Craftsman's Guide to Software Structure and Design (Robert C. Martin Series) (Robert C. Martin)
- Your Highlight on Location 1248-1249 | Added on Tuesday, August 8, 2023 1:16:55 PM
  
  LSP: THE LISKOV SUBSTITUTION PRINCIPLE
  =-=-=-=-=-=-=-=-=-=