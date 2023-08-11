- ## What is Design and Architecture?
	- The measure of design quality is simply the measure of the effort required to meet the needs of the customer. If that effort is low, and stays low throughout the lifetime of the system, the design is good. If that effort grows with each new release, the design is bad. It’s as simple as that.
	- ### Eisenhower's matrix
		- Eisenhower said:
			- I have two kinds of problems, the *urgent* and the *important*. The *urgent* are *not important*, and the *important* are *never urgent*.
		- The ﬁrst value of software -behavior- is urgent but not always particularly important.
		- The second value of software -architecture- is important but never particularly urgent.
		- We can arrange these four couplets into priorities:
			- *urgent* and *important*
			  logseq.order-list-type:: number
			- *not urgent* and *important*
			  logseq.order-list-type:: number
			- *urgent* and *not important*
			  logseq.order-list-type:: number
			- *not urgent* and *not important*
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
	- The best way to understand this principle is by looking at the symptoms of violating it:
		- ### SYMPTOM 1: ACCIDENTAL DUPLICATION
			- My favorite example is the `Employee` class from a payroll application. It has three methods: `calculatePay()`, `reportHours()`, and `save()`
			- {{renderer code_diagram,plantuml}}
			  collapsed:: true
				- ```plantuml
				  @startuml
				  
				  allowmixing
				  left to right direction
				  
				  Title Employee class from a payroll application
				  actor CFO
				  actor COO
				  actor CTO
				  
				  class Employee {
				    +calculatePay()
				    +reportHours()
				    +save()
				  } 
				  CFO ..> Employee
				  COO ..> Employee
				  CTO ..> Employee
				  @enduml
				  yee
				  @enduml
				  ```
				- This class violates the SRP because those three methods are responsible to three very different actors.
					- The `calculatePay()` method is specified by the accounting department, which reports to the CFO.
					- The `reportHours()` method is specified and used by the human resources department, which reports to the COO.
					- The `save()` method is specified by the database administrators (DBAs), who report to the CTO.
				- By putting the source code for these three methods into a single `Employee` class, the developers have coupled each of these actors to the others. This coupling can cause theactions of the CFO’s team to aﬀect something that the COO’s
				  team depends on.
				- For example, suppose that the `calculatePay()` function and the `reportHours()` function share a common algorithm for calculating non-overtime hours.
				- Developers, who are careful not to duplicate code, put that
				  algorithm into a function named `regularHours()`
				- Now suppose that the CFO’s team decides that the way non-overtime hours are calculated needs to be tweaked. In contrast, the COO’s team in HR does not want that particular tweak because they use non-overtime hours for a different purpose.
				- A developer is tasked to make the change, and sees the convenient regularHours() function called by the `calculatePay()` method. Unfortunately, that developer does not notice that the function is also called by the `reportHours()` function.
				- The developer makes the required change and carefully tests it. The CFO’s team validates that the new function works as desired, and the system is deployed. Of course, the COO’s team doesn’t know that this is happening. The HR personnel continue to use the reports generated by the `reportHours()` function - but now they contain incorrect numbers.
			- We’ve all seen things like this happen. These problems occur because we put code that different actors depend on into close proximity. The SRP says to separate the code that different actors depend on.
		- ### SYMPTOM 2: MERGES
			- Two different developers, possibly from two different teams, check out the Employee class and begin to make changes. Unfortunately their changes collide. The result is a merge.
			- merges are risky affairs
			- Once again, the way to avoid this problem is to separate code that supports different actors.
		- ### SOLUTIONS
			- {{renderer code_diagram,plantuml}}
			  collapsed:: true
				- ```plantuml
				  @startuml
				  
				  allowmixing
				  left to right direction
				  
				  Title The three classes do not know about each other
				  
				  class PayCalculator {
				    + calculatePay()
				  }
				  class HourReporter {
				    + reportHours()
				  }
				  class EmployeeSaver{
				    + saveEmployee()
				  }
				  object "Employee Data" as emp_data
				  
				  PayCalculator --> emp_data
				  HourReporter --> emp_data
				  EmployeeSaver --> emp_data
				  
				  
				  @enduml
				  ```
			- The most obvious way to solve the problem is to separate the data from the functions. The three classes share access to `EmployeeData`, which is a simple data structure
			  with no methods. Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided.
			- The downside of this solution is that the developers now have three classes that they have to instantiate and track. A common solution to this dilemma is to use the Facade pattern.
			- {{renderer code_diagram,plantuml}}
			  collapsed:: true
				- ```plantuml
				  @startuml
				  
				  allowmixing
				  left to right direction
				  
				  Title The <i>Facade</i> pattern
				  
				  class EmployeeFacade {
				    + calculatePay()
				    + reportHours()
				    + save()
				  }
				  
				  class PayCalculator {
				    + calculatePay()
				  }
				  class HourReporter {
				    + reportHours()
				  }
				  class EmployeeSaver{
				    + saveEmployee()
				  }
				  object "Employee Data" as emp_data
				  
				  EmployeeFacade --> PayCalculator
				  EmployeeFacade --> HourReporter
				  EmployeeFacade --> EmployeeSaver
				  PayCalculator --> emp_data
				  HourReporter --> emp_data
				  EmployeeSaver --> emp_data
				  
				  @enduml
				  ```
				- The `EmployeeFacade` contains very little code. It is responsible for instantiating and delegating to the classes with the functions.
		- ### CONCLUSION
			- The Single Responsibility Principle is about functions and classes - but it reappears in a different form at two more levels. At the level of components, it becomes the Common Closure Principle. At the architectural level, it becomes the Axis of Change responsible for the creation of Architectural Boundaries.
	- ## OCP: THE OPEN-CLOSED PRINCIPLE
		- A software artifact should be open for extension but closed for modification.
		- In other words, the behavior of a software artifact ought to be extendible, without having to modify that artifact.
		- ### A THOUGHT EXPERIMENT
			- Imagine, for a moment, that we have a system that displays a ﬁnancial summary on a web page. The data on the page is scrollable, and negative numbers are rendered in red.
			- Now imagine that the stakeholders ask that this same information be turned into a report to be printed on a black-and-white printer. The report should be properly paginated, with appropriate page headers, page footers, and column labels. Negative numbers should be surrounded by parentheses.
			- Clearly, some new code must be written. But how much old code will have to change?
			- A good software architecture would reduce the amount of changed code to the barest minimum. Ideally, zero.
			- How?
				- By properly separating the things that change for diﬀerent reasons (the Single Responsibility Principle),
				- and then organizing the dependencies between those things
				  properly (the Dependency Inversion Principle).
			- By applying the SRP, we might come up with the data-ﬂow view shown in
			- {{renderer code_diagram,plantuml}}
			  collapsed:: true
				- ```plantuml
				  @startuml
				  
				  left to right direction
				  
				  Title Applying the SRP
				  
				  card financial_data [ 
				  	Financial Data 
				  ]
				  usecase financial_analyzer [ 
				  	Financial Analyzer 
				  ]
				  card financial_report_data [ 
				  	Financial Report Data 
				  ]
				  usecase web_reporter [ 
				  	Web Reporter
				  ]
				  usecase print_reporter [ 
				  	Print Reporter
				  ]
				  
				  financial_data --> financial_analyzer
				  financial_analyzer --> financial_report_data
				  financial_report_data --> web_reporter
				  financial_report_data --> print_reporter
				  
				  @enduml
				  ```
			- The essential insight here is that generating the report involves two separate responsibilities: the calculation of the reported data, and the presentation of that data into a web- and printer-friendly form.
			- Having made this separation, we need to organize the source code dependencies to ensure that changes to one of those responsibilities do not cause changes in the other. Also, the new organization should ensure that the behavior can be extended without undo modiﬁcation.
			- We accomplish this by partitioning the processes into classes, and separating those classes into components, as shown by the double lines in the diagram in
			- {{renderer code_diagram,plantuml}}
			  collapsed:: true
				- ```plantuml
				  @startuml
				  
				  skinparam linetype ortho
				  
				  package Interactor {
				      together {
				          object "Financial \nReport \nRequest\n<DS>" as financial_report_request
				          interface "Financial \nReport \nRequester" as financial_report_requester
				          object "Financial \nReport \nResponse\n<DS>" as financial_report_response
				      }
				      class "Financial \nReport \nGenerator" as financial_report_generator
				      entity "Financial \nentities" as financial_entities
				      interface "Financial \nData \nGateway" as financial_data_gateway
				  }
				  
				  package Controller {
				      class "Financial \nReport \nController" as financial_report_controller
				      interface "Financial \nReport \nPresenter" as financial_report_presenter
				  }
				  
				  package Database {
				      class "Financial \nData \nMapper" as financial_data_mapper
				      class "Financial \nDatabase" as financial_database
				  }
				  
				  package "Screen Presenter" {
				      class "Screen \nPresenter" as screen_presenter
				      class "Screen \nView \nModel" as screen_view_model 
				      interface "Screen \nView" as screen_view
				      
				  }
				  
				  package "Web View" {
				      class "Web \nView " as web_view
				  }
				  
				  package "Print Presenter" {
				      class "Print \nPresenter" as print_presenter
				      object "Print \nView \nModel\n<DS>" as print_view_model
				      interface "Print \nView" as print_view
				  }
				  
				  package "PDF View" {
				      class "PDF \nView " as pdf_view
				  }
				  
				  web_view -u-|> screen_view
				  screen_view -u-> screen_view_model
				  screen_view_model <-u- screen_presenter
				  screen_presenter -d-> screen_view
				  screen_presenter -u-|> financial_report_presenter
				  
				  pdf_view -u-|> print_view
				  print_view -u-> print_view_model
				  print_view_model <-u- print_presenter
				  print_presenter -d-> print_view
				  print_presenter -u-|> financial_report_presenter
				  
				  financial_report_controller -d-> financial_report_presenter
				  financial_report_controller -r-> financial_report_request
				  financial_report_controller -r-> financial_report_requester
				  financial_report_controller -r-> financial_report_response
				  financial_report_presenter -r-> financial_report_response
				  financial_data_mapper -r-> financial_database
				  financial_data_mapper -u-> financial_data_gateway
				  financial_data_mapper -u-> financial_entities
				  
				  financial_report_generator -l-> financial_report_request
				  financial_report_generator -l-|> financial_report_requester
				  financial_report_generator -l-> financial_report_response
				  
				  financial_report_request -[hidden]d-> financial_report_requester
				  financial_report_requester -[hidden]d-> financial_report_response
				  financial_report_generator -r-> financial_entities
				  financial_report_generator -d-> financial_data_gateway
				  
				  @enduml
				  ```
		- Classes marked with
			- <I> are interfaces
			- <DS> are data structures
			- Open arrowheads are using relationships
			- Closed arrowheads are *implements* or *inheritance* relationships
		- Notice:
			- All the dependencies are source code dependencies.
			- An arrow pointing from class A to class B means that the source code of class A mentions the name of class B, but class B mentions nothing about class A.
			- `FinancialDataMapper` knows about `FinancialDataGateway` through an implements relationship, but `FinancialGateway` knows nothing at all about `FinancialDataMapper`.
			- Each module is crossed in one direction only.
				- This means that all component relationships are unidirectional, as shown in the component graph.
				- These arrows point toward the components that we want to protect from change.
				- {{renderer code_diagram,plantuml}}
					- ```plantuml
					  @startuml
					  
					  component "Financial \nReport \nController" as financial_report_controller
					   component "Financial \nReport \nInteractor" as financial_report_interactor
					   component "Financial \nReport \nDatabase" as financial_report_database
					   component "Screen \nPresenter" as screen_presenter
					   component "Print \nPresenter" as print_presenter
					   component "Web \nView" as web_view
					   component "PDF \nView" as pdf_view
					   
					  web_view -u-> screen_presenter
					  pdf_view -u-> print_presenter
					  screen_presenter -u-> financial_report_controller
					  print_presenter -u-> financial_report_controller
					  @enduml
					  ```
		-
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