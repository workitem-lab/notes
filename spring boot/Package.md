### 3.2. Package & folder structure (MVC layered, prod-ready)
We’ll standardize this so all future services feel the same:

```text
src/
 └─ main/
     ├─ java/
     │   └─ com.workitem.customer
     │       ├─ api/
     │       │   ├─ CustomerController.java
     │       │   ├─ dto/
     │       │   │   ├─ CustomerRequest.java
     │       │   │   └─ CustomerResponse.java
     │       │   └─ mapper/
     │       │       └─ CustomerMapper.java
     │       ├─ domain/
     │       │   ├─ model/
     │       │   │   └─ Customer.java
     │       │   └─ service/
     │       │       └─ CustomerService.java
     │       ├─ persistence/
     │       │   ├─ entity/
     │       │   │   └─ CustomerEntity.java
     │       │   └─ repo/
     │       │       └─ CustomerRepository.java
     │       ├─ config/
     │       │   ├─ WebConfig.java
     │       │   └─ AppProperties.java
     │       ├─ exception/
     │       │   ├─ CustomerNotFoundException.java
     │       │   ├─ ApiError.java
     │       │   └─ GlobalExceptionHandler.java
     │       └─ CustomerServiceApplication.java
     └─ resources/
         ├─ application.yml
         └─ db/
             └─ migration/
                 └─ V1__init_customer.sql

```