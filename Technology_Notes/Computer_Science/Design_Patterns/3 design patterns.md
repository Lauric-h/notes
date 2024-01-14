#learnings #computerscience #concept #designpatterns 

From https://blog.bitsrc.io/3-design-patterns-every-developer-should-learn-71a51568ac9d  

## Strategy 
Open-closed design principle: Code base should be open for extension but closed for modification.

It needs 4 elements:
- Client: where the context is used
- Context: where the is algorithm is chosen at runtime
- Intergace: strategy
- Algorithms: applications

![](https://sourcemaking.com/files/v2/content/patterns/Strategy_example1.png)

Instead of adding more complexities and repeating code, we split algorithm in strategies (independant classes). They all implement a method, and depending on the context, one or the other strategy is used.

```java
interface process PackageStrategy has
	method processPackage(package);

//These strategies implement the algorithm by implementing the interface above.
class SendByRail implements process PackageStrategy has
	method processPackage(package) {
		//process the package that will be sent by Rail and return something
}

class SendByBike implements process PackageStrategy has
	method processPackage(package) {
		// process and return something
	}
!
//strategies used by the context class
class Context {
	private strategy: processPackageStrategy
	
	method setStrategy(processPackageStrategy Strategy) does
		this.strategy= strategy;

	method executeStrategy(Package package) does
		return strategy.processPackage();
}

// read that strategy from user (UI or Api)
class App {
	create a new context instance;
	get package info;
	read the desired user choice

	if (choice is rail) then
		context.setStrategy(new SendByRail())
	if (choice is bike) then
		context.setStrategy(new SendByBike())

	response = context.executeStrategy(package)
``` 

## Singleton
*There is only one instance of a class*  

Main goal => Maintain control over shared resources such as DB, stores and files. 
[[Singleton]]

![](https://ded9.com/wp-content/uploads/2021/05/digrack.com-singleton-design-patterns.png)

## Observer
Enables to set a subscription mechanism that allows other entities to be alerted of each occurence on the entity subscribed.
Example: Kafka, RabbitMQ etc.

One-to-many relationship.

*f code were contributed to a remote repository, a CI environment would monitor it for changes and execute a build*

![](https://sourcemaking.com/files/v2/content/patterns/Observer_example1.png)