
# 🧠 Class level annotation + controller 

```java
@RestController
@RequestMapping("/api/v1/customers")
public class CustomerController {
```
## @RestController 
* Marks the class as a web controller 
* All method return values are written directly to HTTP response body (usually JSON)
* It's a composed annotation of ```@Controller``` + ```@ResponseBody``` , so you don't need to put ```@ResponseBody on each method```
## @RestController – Diagram

```markdown
graph TD

    subgraph SpringMVC["Spring Web MVC"]
        A["@Controller"]
        B["@ResponseBody"]
    end

    C["@RestController"]

    A --> C
    B --> C

    subgraph Usage["When you use @RestController on a class"]
        D["CustomerController"]
        E["Handler Methods<br/>get(), create(), list()"]
        F["HTTP Response Body<br/>(JSON)"]
    end

    C --> D
    D --> E
    E --> F
    
    ```
## @RequestMapping

* ```@RequestMapping``` ("/api/v1/customer"): Defines the base URL path for all methods in this controller.
* Combined with method-level mappings below, it yield endpoints ```/api/v1/customers/``` and ```/api/v1/customers/{id}```

## 🧱 Fied + contructor 

```java
private final CustomerService service;
```
 * Dependency on the business logic layer
 * Final Immutable after construction 

```java
public CustomerController(CustomerService service) {
    this.service = service;
}
```

* Constructor injection: Declares a required dependency, promoting immutability and testability
* How Spring sees ```CustomerController``` needs a ```CustomerService```, finds a bean of type ```CustomerService```, injects it.
* Why constructor injection:
	- Mandatory dependencies are explicit
	- Good for testing (you pass mocks)
	- Avoids field injection drawbacks 
## Create customer (POST)

```java
@PostMapping
@ResponseStatus(HttpStatus.CREATED)
public CustomerResponse create(@Valid @RequestBody CustomerRequest request) {
    return service.create(request);
}
```

```@POSTMapping``` 
* Shortcut for ```@RequestMapping(method = RequestMethod.POST)```. 
* Path: No path specified -> uses the class path
	* Final endpoint: ```POST/api/v1/customers```
* Use it for creating resources, or operations that have side effects and receive a body.
* ```@ResponseStatus(HttpStatus.CREATED)```
	* Forces this method to return HTTP 201 Created if it succeeds
	* REST best practice: On creation, return ```201``` instead of ```200```.
	* Communicates clearly to clients that a new resources was created.
* ```@Valid``` - Triggers bean validation. Tell Spring to validate ```CustomerRequest``` using Bean Validation constrains 
	(```@NotNull```, ```@Email```, ```@Size```, etc.) on that class.
* How 
	* Before the method body runs, Spring 
		1. Deserializes JSON into ```CustomerRequest```.
		2. Runs validation.
		3. If invalid -> throws a ```MethodArgumentNotValidException``` -> usually handled by a ```@ControllerAdvice``` to return a 400 with errors. 
* When to use - On any request body or method parameter that must be validated.

```@RequestBody``` - Bind the HTTP request **body** (JSON) to the `CustomerRequest` object.
* Uses `HttpMessageConverter` (e.g. Jackson) to convert JSON ↔ Java.
* For complex inputs sent in the body: JSON objects, arrays, etc.
* Cleanly separates **transport** (JSON) from **domain** (Java DTO).
#### Method body 

```java
return service.create(request);
```
* Delegates to the service; controller stays thin:
	* Controller = **HTTP layer** (mapping, validation, status codes).
	* Service = **business logic**.