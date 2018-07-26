#Functional Programming

###Why
- Imperative 
- Declarative - What we want rather than delve how to do it.
Concise is short, devoid of noise, and boiled down to its essence to convey the intent effectively.

- Be declarative
- Promote immutability:
	- Mutable code : More things change, easier it is for things to break and creep errors
	- Treat objects as immutable
- Avoid side effects
- Prefer expressions over statements
- Design with higher-order functions

###Basic
- Functional Interface
	- Consumer - apply 
	- Predicate<T> : predicates takes one parameter of type T and returns a boolean result
	- Function<T,R> : functions take a parameter of type T and returns a result R
- type inferance : compiler determines the parametertype based on context
	- infered parameters are not final 		
- method reference ::
	- instance methods
	- static methods
	- methods with parameters
	- cannot use if we have to manipulate the parameters before calling the method or change the result

### Features
- forEach
	- cannot break out of the iteration
- map
	- returns a new collection
- filter
	- excepts method which returns a boolean
	- if true element added to collection else skipped
	- use predicates to avoid repeating yourself
		- Closure (lexical scoping): Lets us cache values in one context and later use in another context					
		
		```java	
			
			//Function returns another function		
			public static Predicate<String> checkIfStartsWith(final String letter){
				return name - > name.startsWith(letter);
			} 
			/*name is passed to the function returned by checkIfStartsWith ... 			
			checkIfStartsWith caches the letter passed in its scope and makes it available 			
			in the returned function*/
			friends.filter(checkIfStartsWith("K"))
			
		```
- reduce
	- method to compare two elements against each other and pass along the result for further comparison with the remaining elements in the collection

- mapToObj 
	- change stream type from IntStream, DoubleStream, LongStream to Stream ... without boxing to Stream<Integer>
		
- sorting
	- use Comparator functional interface
	- parameter-routing conventions
		- first parameter id target and second is used as its argument
	```java
	
		.sorted((person1, person2) -> person1.ageDifference(person2))
		
		//method-reference
		.sorted(Person::ageDifference)
		
	```
- Java compiler follows a few simple rules to resolve default methods:
	1. Subtypes automatically carry over the default methods from their super-types.
	2. For interfaces that contribute a default method, the implementation in a subtype takes precedence over the one in supertypes.
	3. Implementations in classes, including abstract declarations, take prece- dence over all interface defaults.
	4. If there’s a conflict between two or more default method implementations, or there’s a default-abstract conflict between two interfaces, the inheriting class should disambiguate.
		
- Lambda expression cannot throw checked exceptions
		
### Design patterns

- Strategy
	- passing functional interface
- Decorator
	- reduce
	- combine
- Builder - loan pattern	
	- passing consumer to a function which accets an object having method chaining (done by returning object itself - this) 
- execute around method pattern
	- Use functional interface passed to a method to wrap around the execution of the function