# Design Principles
[Core Design Principles for Software Developers](https://www.youtube.com/watch?v=llGgO74uXMI&t=4815s)

- Keep it simple
  - Simple keeps you focused
    - Declarative code is more simple then Imperative code 
      - Imperative code: you tell the compiler what you want to happen, step by step
      - Declarative code: you write code that describes what you want, but not necessarily how to get it 
  - Solves only real problems we kown about
  - Easier to understand
> Simple is not Familiar 
- Complexity
  - inherent and accidental
    - inherent: complexity of the problem (domain)
    - accidental: comes from solution of the problem eg: Concurrency

> Good Design hides inherent complexity and eliminates the accidental complexity
 

- YAGNI - You ain't going to need it (yet)
  - Avoid doing a code untill you no longer can avoid it
  - To postpone we need good Automated testing


- High Cohesion and Low Coupling
  - Cohesive code - Narrow, Focused and does one thing really well
  - Coupling - what you depend on
    - Inheritence - increases coupling
    - Try to remove coupling
    - Make it loose instead of tight
      - Depending on an interface is low coupling
      - Depending on a class is tight coupling


- DRY - Do not repeat yourself (code and effort)


- Single Responsibility Principle
  - Cohesive code
  - Short methods
  - SLAP - Single level of Absraction
    - Don't comment What, instead commet Why
  - Compose Method Pattern
    - Code should be composed of the steps you wnat to take in developing the logic
    - Self documenting
 
 
- Open-Close principle (OCP)
  - Open for extension but closed from modification
  - Abstraction and polymorphism


- Liskov's substitution principle
  - Inheritance should be used only for substitutability
    - If an Object of B should be used **anywhere** an object of A is used then use inheritance
    - If an Object of B should be **use** an object of A, then use composition / delegation		
  - **User of the base class should be able to use an instance of the derived class without knowing the difference**
      - **Services of the derived class should require no more and promise no less than the corresponding services of the base class**
      - public vs protected in base vs derived
      - derived function can't throw a new checked exception not thrown by the base class (unless the new exception extends the old one...) 
      - collection of derived does not extend from collection of base
  - Use composition or delegation instead of inheritance unless you want substitutability
    - In Java this may violate DRY , OCP		
    - Using Groovy @Delegate does not viloate DRY, OCP as its **compile time** meta programming		


- Dependency inversion principle - Decouple
    - Class should not depend on another class, they have to depend on an abstraction (interface)


- Interface segregation principle - Keep interfaces Cohesive
  - Cohesion, Single responssibility principle at an interface level
  - Make the interfaces narrow focused and cohesive
