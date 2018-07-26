#Microservices

Stategic Goal --> Architectural Principles --> Design and delivery practices

- Loose coupling:
A loosely coupled microservice knows as little as it needs to about the service with with it collaborates.
	- Limit number of different type of calls from one service to another
	
- High Cohesion:
Find boundaries within our problem domain that help ensure that related behaviour is in one place

- Bounded context (Domain Driven Design):
	- Context means a specific responsibility
	- Bounded context means that responsibility is enforced with explicit boundaries
	
	
- Avoid breaking changes
	If a microservice adds new fields to a piece of data it sends out, existing consumers shouldn't be impacted
- Keep your APIs Technology-Agnostic
	Keep the APIs used for communcating between microservices technology-agnostic
- Make your services simple for consumers
	Allow our clients full freedom in their technolog choice
		ex: We might use client libraries to make it easy for consumers, but this can come at the cost of increased coupling
- Hide internal implementation detail

> Be conservative in what you do, be liberal in what you accept from others

- Schematic versioning
	- MAJOR.MINOR.PATCH
		- MAJOR: backward incompatible changes have been made
		- MINOR: new functionality added that should be backward compatible
		- PATCH: bug fixed made to existing functionality
