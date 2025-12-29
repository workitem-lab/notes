
### Level 1 — OOP Foundations 

[[https://github.com/workitem-lab/java-oop.git]]

Classes & Objects
	- state - fields, the data the object holds (fields like `balance`, `accountNumber`)
	- behavior - methods, what the object can do (methods like `deposit`, `withdraw`)
	- construction -methods 
	- identity vs equality - object references 
	
1) Class - the blueprint -> definition of what something has and does 
	- Class: ```Customer``` 

2) Object -a real instance created from the blueprint
	- Object: ```New Customer("yourName", "yourAge")```

3) Fi
Notes 
- final - is compile-time modifier that enforces immutability of references, methods or classes depending on where its applied
	- A variable declared `final` can be assigned only once
	
	- Implications 
	
		-For primitive types: the value itself cannot change 
```
final int x = 10;
x = 20; // ❌ compile error
```
		
	- For **object references**: the reference cannot point to a new object, but the object’s internal state can still change (unless the object itself is immutable).
		