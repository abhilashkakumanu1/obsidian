Design patterns are solutions for commonly occurring problems. Algorithms are kind of similar to design patterns but algorithms are clear set of actions to solve the problem while design pattern is more like a high-level description of a solution.

1. **Strategy pattern** - Instead of implementing a single algorithm directly, code receives run-time instructions as to which in a family of algorithms to use. It is a behavioral pattern because it is concerned with the assignment of responsibilities between objects. => **Dependency injection**

	It just says - 'prefer composition over inheritance'. Inheritance is `is a` relationship, where as composition is  `has a` relationship. We can think of inheritance as a vertical hierarchy where child gets (or has to implement) everything parents has whether they need it or not. Sometimes we might want to reuse the same method logic across siblings or something that doesn't directly belong to vertical hierarchy or maybe we don't want everything from parent. Things get messy when our needs turn 2-dimensional. Instead of separating this shared behavior into a independent class and inheriting from it (this might not be a great idea cause we are never sure of the future requirements and this way, we might have to create new inheritance structure => results in changing the previous code to implement new feature - breaking Open/Close principle) we could have thought of each behavior as a composition (made up of) of behaviors - like lego pieces. 
	Also, we can inherit from a class which takes in these concrete implementations as arguments (types of the parameter can be specified at prior hand by using interfaces). 
	
	So, this simply says that rather than hard-coding the behavior into the parent class and inheriting from it to "reuse" the code, we should think of a object as a combination of functionality (like Lego pieces). So, instead of 'inheriting' all the behavior from the ancestors (which might not contain everything you need), you should cherry pick the behaviors that you need.
	
	**Use case**: sort function in some programming languages (ex: javascript) lets you specify the sorting behavior at run-time instead of hard-coding implementation of any particular sorting algorithm

2.  **Observer pattern** - pub/sub model => when you have to notify multiple things when a state changes
	
	This is same as the `push vs poll` problem is networking. polling means asking - are we there yet? are we there yet? This is obviously inefficient as we have to make a lot of calls (the size of interval is dependent on the business needs) and when there multiple such subscribers number of requests increase crazy fast. 
	In order to solve this issue we use pushing instead of polling. pushing means when ever there is an update in the state, the observable (publisher) pushes (notifies) the new state to all the observers. 
	
	Generally, observable have `add(IObservable), remove(IObservable), notify() ` methods on it to register, de-register and notify the observers respectively. Also, observer should have a `update` method on it, which gets called after notification comes. There most probably will be `getState` and `setState` methods as well on the observable. 
	
	Some implementations (like in head first design patterns) may include passing the concrete observable object it self as a argument for the constructor function of observable.
	
	**Use case**: Node internally implements observer pattern for its event-driven architecture => callbacks with first argument as event type ("on", "click", "submit", etc) and the second argument as a function which gets `added` to an array on the observable. All the elements are called (be passing state as an argument (event object in the case of DOM)) whenever that event occurs.
	
	**Note**: Generally, many languages doesn't support inheriting from multiple classes but support implementing multiple interfaces
	
	Calling a method on an object is like sending a 'message' to that object and clear method makes it clear what message we are sending.
	
3. **Decorator pattern** - This can be looked at in 2 ways : 
	1. Attaches additional responsibilities to an object dynamically (run-time). It is a flexible alternative to sub-classing. 
	changing the behavior of an object (on calling a method) at run-time (without opening the class and changing its contents) => wrap the object inside (called as component) with a wrapper object (called decorator) which communicates with the outside world. The outer decorator objects are of same type as the component (they are interchangeable) - so it is both `is a` and `has a` 