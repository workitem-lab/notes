***Service layer with transactions***

This is where business logic lives and where we put ```@Transactional``` 
Service is a domain-level orchestration layer 

- API DTOs (`CustomerRequest`, `CustomerResponse`)
- Domain model (`Customer`)
- Persistence layer (`CustomerEntity`, `CustomerRepository`)
- Mapping layer (`CustomerMapper`)
- Exception handling (`CustomerNotFoundException`)

**1. Class Setup**

```java
@Service
public class CustomerService {
```

- ```@Service``` registers this as a Spring bean 
- It represents a domain service, not HTTP or persistence concerns.

**2. Dependency Injection**

```java
private final CustomerRepository repository;

public CustomerService(CustomerRepository repository) {
    this.repository = repository;
}
```

- Constructor injection ensure immutability and testability 
- ```CustomerRepository``` is the persistence abstraction.

### Create 

```java
@Transactional
public CustomerResponse create(CustomerRequest request) {
    CustomerEntity entity = CustomerMapper.toEntity(request);
    CustomerEntity saved  = repository.save(entity);
    Customer domain       = CustomerMapper.toDomain(saved);
    return CustomerMapper.toResponse(domain);
}
```

### what happen 

- Map request -> entity
	-Converts API input into a persistence-ready object
- Save entity 
	-Uses Spring Data JPA to persist the customer 
- Map entity  ->  domain 
	-Converts persistence representation into a domain model
- Maps domain -> response 
	- 