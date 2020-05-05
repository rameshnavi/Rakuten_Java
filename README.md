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
================================================================

Day 2
------
	Recap:
		instance variables ==> Heap Area
		static variables ==> Class Variables ==> Class Data
		local variables ==> Stack

		instance methods ==> using objects to invoke them
			==> implicit "this" as first argument
		static methods ==> using class to invoke them
			==> can't access "this"

		--------
		Package: Logical Grouping of classes
		Inheritance
			Generalization and Specializtion relationship
			"extends" keyword is used to inherit
			-> Polymorphism and dynamic binding [ isExpensive()]
		Relflection API
			--> We invoked methods
	---------------------------------------

	Few classes are too generic, objects of such type doesn't exist in real world, but they are meant only for
	Generalizzation.
		Account, Product

		Such classes should be marked as "abstract". Once the class is marked "abstract", you can't instantiate

		abstract class Product {

		}

		Product p = new Product(); // compilation ERROR

		class Mobile extends Product {} // valid
		new Mobile()

		===========

		
			Product.java

			public boolean isExpensive() {
				return false;
			}

			Abstract Methods:
			Methods which doesn't have body

			Product.java

			public abstract boolean isExpensive(); // in C++ it's called pure virtual machine

			Why to have this method in Product.java
				1) We can achieve Polymorphic behaviour
					for (Product p : products) {
						if (p.isExpensive()) {

				2) Enforce all inherited class to compulsorly override this method

		==========

			Why in Object.java
				equals() is not made abstract?
				this method is useful only for entities and not for any other type of objects

		=============

		Realization Relationship
			A component/Object will realize the specification/protocols defined by other in order to communicate

			In Real world 2 different types of objects are communicating with the help of "interface"
				--> HDMI, VGA, USB, COM, LPT

				Mechanism used by each object to generate/consume might be different

		In Software Industry we use "interfaces" to establish communication between different objects.

		How does an interface look like in Java:

			interface interfaceName {
				constants
				abstract methods
			}


			interface EmployeeDao {
				void register(Employee e);
				//boolean login(String username, String password);
			}

			All methods in interface are "public" and "abstract"

			public abstract void register(Employee e);

			class EmployeeDaoMySQLImpl implements EmployeeDao {
				public void register(Employee e) {
					// logic
				}
			}

			// implements -- > Realize
			class EmployeeDaoMongoImpl implements EmployeeDao {
				public void register(Employee e) {
					// logic
				}
			}

			Why program to interface?
				a) DESIGN
				b) IMPLEMENTATION
				c) TESTING
				d) INTEGRATION
				e) loose coupling

			=====================
			Issues with changing code in client:

			1) In real-world clients are many
			2) clients are of different kinds : Mobile, Web, Standalone
			3) Exposing which type of logic is used to client


			Solution:
				Lets have a configuration file, which can be used by all types of clients

			===========

			Factory classes: are classes which create objects and return

			MobileDao dao = new MobileDaoSqlImpl();

			change to

			MobileDao dao = MobileDaoFactory.getMobileDao();

			-------
			We have read the class name from properites files

			We need to create object of this

			If we know the class name in advance:
				new ClassName()
				new Product()
				new MobileDaoSQLImpl();

			--
			If we don't know the class name in advance i can still create object using Reflection APIs

			String NAME = "com.rakuten.prj.dao.MobileDaoSqlImpl";

			Class.forName(NAME); // loads the class into JVM

			OR
				// create an object of class [ refered by NAME ] which is loaded
				Class.forName(NAME).newInstance();

=========================================================================
	Product[] products = new Product[5]; // Array of 5 Pointers
		products[0] = new Tv(133, "Sony Bravia", 135000.00, "LED"); // upcasting
		products[1] = new Mobile(453, "MotoG", 12999.00, "4G");
		products[2] = new Tv(634, "Onida Thunder", 3500.00, "CRT");
		products[3] = new Mobile(621, "iPhone XR", 99999.00, "4G");
		products[4] = new Mobile(844, "Oppo", 9999.00, "4G");

	String[] names = {"George","Aamir","James","Bharath"};

	int[] nos = {56,22,6,2,772};

	We need to sort them. What do you do?
		We compare.

		for sorting, finding max, min we should have the objects capabale of compare

		a.compareTo(b); // method can return a number, if returned values >0, <0 or ==0


		//OCP
		void sort(Comparable[] elems) {
			for(i = 0; ....) {
				for(j = i+1; ....) {
					if(elems[i].compareTo(elems[j]) > 0) {
						// swap logic
					}
				}
			}
		}

	============================================================

	interface Dance {
		dance();
	}

	interface Fight {
		fight();
	}

	interface Swim {
		swim();
	}

	// Actor is capable of dancing
	class Actor implements Dance {
		dance() { // ...}
	}

	// hero is a actor, every actor knows to dance
	// hero should alos know to dance
	// Hero is also capable of fighting and swiming
	class Hero extends Actor implements Fight, Swim {
		fight() {}
	 	swim() {}
	 }

	 ======================================================================================================

	 Generic classes: <>

	 Generic type can only be object type, not primitive

	 public class Rectangle <T> {
	 		T width;
	 		T breadth;

	 		//
	 }

	 Rectangle<Integer> r1 = new Rectangle<Integer>(4,5);

	 Rectangle<Double> r2 = new Rectangle<Double>(1.4,3.5);

	 Rectangle<String> r3 = new Rectangle<String>("Hello","World");

	 ---------

	 class IRectangle {
	 	int width;
	 	int breadth;
	 }

	 class DRectangle {
	 	double width;
	 	double breadth;
	 }
============================================================================================================

	Note on Exception handling:

	An abnormal condition that arises during program execution is an exception.

	In Java, exception is an object. It gives me the following details:
		a) What went wrong
		b) Why
		c) Where

	==========

	Handle exceptions in 2 ways:

		1) conditional statement [ Recommended]
				int x = 10;
				int y = 0;
				if(y != 0 ) System.out.println("Result : " + (x/y));

		2) try-catch syntax
				try {
					int x = 10;
					int y = 0;
					System.out.println("Result : " + (x/y));
				} catch(ArithmeticExeption ex) {
					s.o.p("problem :-(");
				}
==================================

		Exceptions can be classfied as Checked or Unchecked.

		Unchecked exceptions happen for reasons with JRE.
			--> divide by zero
			--> Null Pointer exception
				Product p; // new Product();
				p.setId(1); // NullPointerException
			--> ArrayIndexOutOfBoundsException
				int[] elems = {5,6};
				int x = elems[3]; // we have only 0 and 1 index

			--> handle it with conditional statement

		Checked exceptions are a result of issues outside JRE
			--> SQLException
				Uniquekey constraint
				Connection down

			--> IOException
				filenotfoundexception
				SocketConnection
			--> ClassNotfoundException

			--> should be handled using try-catch
==============================================================
	
	Resume @3:00 after Lunch Break

	---------------------------------------------
	Java Collection Framework [ DataStructures]

    Data Containers: array is a data container

    int[] data = new int[400];

    String[] names = {"a","b","c"}

    Limitations:
    	a) Size is fixed, it can't grow nor shrink
    	b) need contiguous memory location
    	c) adding/removing from arbitrary position is difficult

    	in an array of size 400, if i need to add an element at 100th postion, we need to move all elements after 100th

    Java Collection Framework --> Data Containers --> DataStructures
    	1) interfaces
    	2) implementation classes
    	3) Algorithm / utility classes

    	----
    	String[] names = {"George", "Angelina", "Brad", "Lee", "Chris"};

    	Comparable is for natural comparison, this will be a part of object
    		Product, String had comparasion code [ compareTo()]

    	Comparator is for custom comparison, generally this code goes in client
    		logic is in client


    	Sorted order: Angelina, Brad, Chris, George, Lee [Natural ] ==> Comparable

    	why not: Lee, Brad, Chris, George, Angelina [ Custom] ==> Comparator

    	-------------------------------------------------------

    	public interface Comparator<T> {
    	    int compare(T o1, T o2);
    	}

    	class LengthComparator implements Comparator<String> {

    		public int compare(String o1, String o2) {
    			return o1.length() - o2.length();
    		}
    	}

    	String[] names = {"George", "Angelina", "Brad", "Lee", "Chris"};
		
		//Arrays.sort(names);

		Arrays.sort(names, new LengthComparator());

		---------

		Anonymous class: 
			a class without a name
			==> can be created using an interface / abstract class

			new Comparator(); // ERROR, you can't create object of interface

			new Comparator<String>() {
				public int compare(String o1, String o2) {
    				return o1.length() - o2.length();
    			}
			}
			----------------------


			class Employee {
				firstName;
				lastName;
				email;
				age;
			}
			FirtNameComparator.java
			class FirtNameComparator implements Comparator {

			}
			LastNameComparator
			class LastNameComparator implements Comparator {

			}
			EmailComparator.java
			class EmailComprator implements Compartor {

			}

		----------------------

		interface Flyable {
			void fly();
		}

		class Bird implements Flyable {
			state and behaviour
			public void fly() {

			}
		}

		class AeroPlane implements Flyable {
			state and behaviour
			public void fly() {

			}
		}

		Flyable f1 = new AeroPlane();

		Flyable f2 = new Bird();

		Flyable f3 = new Bird();		


		Flyable f = new Flyable() {
			public void fly() {
				try jumping from 10th floor!!!
			}
		}

		============================

		Java 8 introduced Lambda expression as a shorter form for anonymous class.

		interface Flyable {
			void fly();
		}

		//Anonymous class
		Flyable f = new Flyable() {
			public void fly() {
				try jumping from 10th floor!!!
			}
		}

		Java 8 Lambda expression:
		Flyable f =  () -> {
				try jumping from 10th floor!!!
			};

		Limitation:
		Lambda's can be used only on FunctionalInterface. 
		A FunctionalInterface is one which has only one method to be 
		defined.

		---------------


		Collections are Iterable

		Iterator has the follwoing methods: ptr = first; ptr != null; ptr = ptr = ptr->next
			boolean hasNext();
			Object next();
			Object remove();

		============================

		List 										Set
	1) supports duplicates 							Unique
	2) index based operations support 				not-supported

		list.remove(20);
		list.add(3,"A");
		list.get(34);
	3) ordered 										not-ordered
	4) re-order
		sort, shuffle, reverse 						does not support


		class ArrayList implements List {

		}

		class LinkedList implements List {

		}


		List list = new ArrayList();
		List list = new LinkedList();
		List list = new ApacheList...();

		----------

		Bad Code:
					List list = new ArrayList();

					list.add("a");
					list.add(3);
					list.add(new Product());

					This collection is not typesafe

					for(Object o : list) {
						if(o instanceof String) {
							String s = (String) o;
						} else if( o instanceof Product) {
							Product p = (Product) o;
						}
						...
					}
		Good Code:
				List<String> list = new ArrayList<>();

				list.add("a");
				list.add(3); // error

		-------------------------------------------------------------------

		Functional Style of Programming
		--------------------------------
			OOP
				methods are tightly coupled to state of object
				deposit(double amt) {
					this.balance += amt;
				}


			Functional Style of programming
				logic is independent of any objects
				uses high Order functions.


		High Order Functions:
			a) Functions which accept other functions as arguments
			b) function returns a function

			--> Treat function as first-class member similar to primitive or object
			======================================

		List<Product> products = new ArrayList<>();
		products.add(new Product(645, "Hp Laptop", 135000.00, "computer"));
		products.add(new Product(224, "iPhone", 98000.00, "mobile"));
		products.add(new Product(834, "Logitech Mouse", 600.00, "computer"));
		products.add(new Product(5, "Sony Bravia", 125000.00, "tv"));
		products.add(new Product(912, "One Plus", 32000.00, "mobile"));
		products.add(new Product(88, "HP Printer", 19000.00, "computer"));


		predicate = (p) -> p.getCategory().equals("mobile");

			filter(elems, predicate) {
				create an empty container;
					loop thro elems
						if predicate
							add to container;
					end loop
				return container;
			}	

		=========================

		Commonly used HOF:
			a) filter
				subset
			b) map
				transform the data
			c) reduce
				to get aggregate
					like [ sum, count, avg, min, max]
			d) forEach
				to consume
			c) collect
				data comming from stream collect into a container
			d) skip
			e) limit

		================

		Java 8 pre-defined functionalinterfaces:
			Predicate, 	Function, BiFunction, Supplier, Consumer

			Predicate:

			Predicate p = (arg) -> true;

		In JAva HOF can be be applied on streams 
		Stream is a channel along which data flows [ Network, Database, File, Collection]

	============

		Terminal functions: collect, reduce, forEach
		Intermediary functions : map, filter, flatMap, skip , limit


	find total of all mobiles?
	



