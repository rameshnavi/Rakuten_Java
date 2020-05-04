# Rakuten_Java

Java Training


Banuprakash C


banuprakashc@yahoo.co.in


banu@lucidatechnologies.com
-----------------------------------

Softwares Required:
	For Java: [ 3 days ]
		1) JDK 8
		2) Eclipse for JEE 2020

	For Spring Boot: [ 3 days]
		1) Maven
		2) Postman
		3) Chrome Browser
		4) Docker
		5) MySQL on Docker or local installation

Timings:
	10:00 - 1:00 and 3:00 - 6:00
 
Pretest link: https://evalground.com/code4/#/publicview/test/candidate/token/ksapqivy

============================================================================================

OOP ==> Object Oriented Programming
		Writing programs/ applications which resemble real world.
		Real World:
			Objects ==> State and behaviour.
			SavingsAccount is an object.
				balance --> state
				How is this balance going to change? Need some actions ==> behaviour ==> messages
				[ credit / debit ]
			---
			Objects communicate with each other by sending a message. What messages an object can accept is exposed thro its interface [ Remote]. What messages an object can accept is exposed thro its interface. We don't need to know how it works, but we need to know what it does.

		OOP should follow SOLID Design Principles:
			S --> Single Responsibility	
					Every object created / manufatured should have one central purpose. What does it take as input and what does it produce.
					Bad Code:
					class A {

					}
			O --> Open Close Principle
					Every component / Object should be closed for a change, open for extension

			L --> Liskov Substitution Principle [ Later..]
			I --> Interface Segregation

				BankingApplication has different interfaces. Customer interface is 
				different from that of a Manager interface
			D --> Dependency Injection
				Tv needs Power Supply
					Does Tv go in search of Power, or is it injected?
					It's Injected
				Tv needs HDMI
					HDMI signal is injected

			We developers do this:
				UI --> Service --> DAO [ Repository code] --> Database connection

			With DI we need to inverse the flow:
					UI <-- Service <-- DAO [ Repository code] <-- Database connection

			 =========================================================================

			 Objects of OOP. 

			 Mechanism to create software objects just like blueprints in real-world

			 JavaScript	< ES5: functions as templates / blueprints

			 		function Person {

			 		}

			 		var p = new Person(); // p is an object of type Person

			 C++ / Java:
			 	class Person {

			 	}

			 	Person p = new Person(); 


			============================================================================

			Java --> Platform to execute bytecode

			Bytecode is a compiled code.

			To generate bytecode we write code in different programming languages and use different compilers


			Java Program language 				Java Compiler 					Bytecode
 
			File.Java 							javac                           compiled code

			Kotlin Program lang 				Kotlin Compiler 				compiled code
			Groovy Program lang 				Grrovy Compiler  				compiled code

			--------

			Bytecode generated is portable
			------

			JDK --> Java Development Kit, --> Java as programming language to build bytecode

			===================================================================================

			Account.java
			public class Account {
				private double balance; //state

				public void deposit(double amt) { // (Account this, double amt)
					balance += amt; 				// this.balance += amt
				}
			}


			javac Account.java ====> Account.class [ Bytecode]
--------------------------
			AccountTest.java

			public class AccountTest {
				public static void main(String[] args) {
					Account first = new Account(); // new is like malloc, dynamic memory allocation
					Account sec = new Account();
					first.deposit(5000); // ctx.message(parameter) ==> deposit(first, 5000)
					second.deposit(3000); // deposit(second, 3000);
				}
			}

			javac AccountTest.java ==> AccountTest.class


		Execute: java AccountTest 

-----------------------

			This starts JRE which in-turn invokes ClassLoaders
				ClassLoaders has the following functions:
					findLoadedClass()
						Check if bytecode is already loaded or not
					loadClass()
						loads bytecode from secondary storage to primary
						It checks:
							a) Current folder where you execute the command
							b) check CLASSPATH env variable
							set CLASSPATH=c:\mycode;d:\mylibs;

					findSystemClass()
						If loadClass() is not able to load [ It didn't find it in CLASSPATH]
						findSystemClass() loads it from APIs.
						When we refer a Machine as Java Enabled:
							1) should have Java Platform [ JRE support]
							2) Should provide APIs [ String, System, Util class]
								"rt.jar"
					defineClass()
						--> .class file is made compatable to target machine [ JVM ]
						JVM is different for different Architecture/OS
	---------------------

	Eclipse --> Open Perspective --> Java

	---------------------

	Access Modifiers:
		private: state should be made private
			private members are not accessable outside of the class
		methods: behaviour should be prefarable public
			actions are done by other classes, hence it has to be exposed

	---------------------------------------------------------------------------

	Constructors:
		Are like special methods which gets invoked as and when object is created.
		Constructors code executed only once when object is created, it can't be explicitly called

		Methods Example: deposit()
		first.deposit(5555);
		first.deposit(2244);

		---------

		Constructors 
			1) same name as that of class
			2) No explicit return type

			compilers create default constructor [ NoArgs] if we don't explicitly write any.

		--------------------

		We need to track how many account instances are created?


		third.getCount();

		compiler converts this into
		Account.getCount();

		So no impilicit "this" pointer for getCount()

		----------

		In a method if we don't use a state, make such methods static.

		constructors for init
		getters for accessor
		setters for mutation
======================================================================

	"new" keyword to create objects
	constructors
	"this" keyword
	instance variables, static variables, instance methods and static methods

=======================================================================

	Object identity:

		Product p1 = new Product(1,"iPhone");
		Product p2 = new Product(1,"iPhone");
		Product p3 = p1;

		Contents of p1 and p2 are same but they are 2 different objects

		(p1 == p2) evalutes address location and returns false

		(p1 == p3) evaluates to true becuase both have same address

		p1.equals(p2) should evaluate to true because both have same content

		== on primitive values checks data, on objects checks references
		hence we should provide equals() to check contents of objects


		Every class inherits from built-in Object.class
		Object class has methods like equals, hashCode, wait, notify, toString

		The method equals() in Object class is working same as ==

	==========================================================================

	Logically grouping of objects/classes from Java's perspective

		1) Entity / Domain / Model classes
			These classes represent business data, no logic in these classes
			Business data should be long lived, beyond the life of appliation
			Generally they are stored in some persistence [ RDBMS, NoSQL, CSV, Files]
			Examples of such classes.
				Rakuten Shopping application
					Customer, Product, Order, Items, ShippingAddress, Payment, ..

				Most of the cases:
				class per table
				fields mapping to columns

			These types of classes should have 
				a) instance variables mapping to DB columns		
				b) constructors
				c) setters / getters
				d) equals()

		2) DAO classes [ Data Access Objects] ==> .NET refers to this DAL ==> Data Access Layer
			they should contain CRUD operations
			CREATE, READ, UPDATE and DELETE 
		3) Business class --> Business logic
		4) Service classes
			acts as a facade over DAO and Business
		5) UI
			--> User Interface classes for Standalone, Web, Mobile, 
		6) Utility classes
			--> Helper classes
			i18N ==> Date/ Currenny has to be converted to different formats based on client location
			Conversion can happen in client before printing. Or can happen in DAO before storing
			Sorting => Client can sort, or I can sort and store


		Scenario:
			An Employee applies for Loan
			DAO will fetch data from "employees" table
			UI will pass the loan amount
			Service will pass the "employees" data and loan amount to "business" class, which does some validations
			--> eligibility, EMI tenure

		============

		In Java we group these classes into packages.
		Package is logical grouping of classes/ folders
			com
			 |
			  Rakuten
			  		|
			  		projectname
			  				|
			  				entity
			  				|
			  				dao
			  				|
			  				service
			  				|
			  				ui

		Without packages codes are not reusable
		It helps avoid clash in same class names coming from different packages

		java
			|
			util
				|
				Date.class
			|
			sql
				|
				Date.class

	java.util.Date d1 = new ...

	java.sql.Date d2 = 

	==================================================================================================

	Relationship between objects
		1) Generalization and Specialization
		2) Realization
		3) Association
		4) Uses A 

		========================

		Java Tools:
			--> Sonar
				Static Code Anaylis
					[CheckStyle + PMD]
				Checkstyle: checks Coding conventions [ Naming Conventions, Spaces, Comments]
				PMD: Coding Stds.
					==> empty conditional statement, empty exception handling code, unreachable code,
						copy and Paste
			--> Maven
				Manages dependecies
			--> Jenkins
					CI/CD
			--> Junit and Mockito
					Unit testing
			--> Clover/ CodeCoverage
					Checking how much of code is tested



			====

			Sonar complains its copy/paste code
				setId() getId() setName() getName() setPrice() getPrice() present in both Tv and Mobile

			=========

			DRY principle -> Don't Repeat Yourself

			for DRY Which relationship to apply
			========================================

			goto shop, point to mobile and ask 
					What's the cost of Product?

			point to TV and ask
					Is this Product for Sale?

			Mobile and Tv generalized form is Product
			and Every Product is a Object


				point to TV and ask
					Is this Object working?

				This leads to IS A relationship

				TV is a Product is a Object
				Mobile is a Product is a Object

			------


			In JAva we use Inheritance to acheive Genralization and Specialization Relationship

			What do you keep in your pocket?
				She replies keys, Tv

				Next Question Tom Alter [ Taylor]
					then I should stich 14" or 32" pockets

			Mistake by the Lady:
				She used IS A Relationship in wrong place

				It should have been:
					Mobile has a Tata Sky TV app

		==============================================================================
		extends keyword for inheritance ==> IS A relationship

		class Product {

		}

		class Mobile extends Product {

		}

		class Tv extends Product {

		}

		=====================
		class Product {
			public double getPrice() {
				return 100;
			}
		}

		class Mobile extends Product {
			@Override
			public double getPrice() {
				return 500;
			}

			public String getConnectivity() {
				return "4G";
			}
		}

		Product p = new Mobile(); // upcasting

		p.getPrice(); // ? What is the return value? 500

		p.getConnectivity(); // output? ERROR Because Product doesn't understand the message

		=============================================

		class Product {
			public Product() {
				prints "P1"
			}
			public Product(int id) {
				prints "P2"
			}
		}

		class Mobile extends Product {
			public Mobile() {
				prints "M1"
			}
			public Mobile(int id, String connect) {
				prints "M2"
			}
		}

		new Mobile(); // P1, M1
		new Mobile(100, "4G"); // P1, M2

		===========

		class Product {
			public Product() {
				prints "P1"
			}
			public Product(int id) {
				prints "P2"
			}
		}

		class Mobile extends Product {
			public Mobile() {
				prints "M1"
			}
			public Mobile(int id, String connect) {
				super(id);
				prints "M2"
			}
		}

		new Mobile(); // P1, M1
		new Mobile(100, "4G"); // P2, M2

		=======================

		In JVM whatever is allocated on HEAP area will have default values.
			int == 0
			double 0.0
			pointers ==> Null

		Tv tvs = new Tv[1000];

		Mobile mobiles = new Mobiles[5000];

		for(Tv t : tvs) {

		}

		for(Mobile m : mobiles) {

		}

		WashingMachine wms = new WanshingMachine[100];
		for(WashingMachine m : wms) {

		}

		Java Reflection API ==> RTTI


		for(Method m : methods) {
			m is a pointer to a method [ getId(), getName(), .....]

			// p.m(); invalid where m is a method
			Object ret = m.invoke(p);


			// normal method call is
			obj.method(); ==> p.getId()
		}
