
# 🧠 Class-level annotation + controller 

```java
@RestController
@RequestMapping("/api/v1/customers")
public class CustomerController {
```
### @RestController 
* Marks the class as a web controller 
* All method return values are written directly to HTTP response body (usually JSON)
* It's a composed annotation of ```@Controller``` + ```@ResponseBody``` , so you don't need to put ```@ResponseBody on each method```
### @RestController – Diagram

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
### @RequestMapping

* ```@RequestMapping``` ("/api/v1/customer"): Defines the base URL path for all methods in this controller.
* Combined with method-level mappings below, it yield endpoints ```/api/v1/customers/``` and ```/api/v1/customers/{id}```

### 🧱 Fied + contructor 

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

