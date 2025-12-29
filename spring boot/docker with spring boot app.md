
### Option A: App runs locally, Postgres runs in 

```yaml
spring:
  application:
    name: customer-service

  datasource:
    url: jdbc:postgresql://localhost:5432/customerdb
    username: customer
    password: customer

  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        format_sql: true

server:
  port: 8081

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics
  endpoint:
    health:
      probes:
        enabled: true

---

spring:
  config:
    activate:
      on-profile: dev

logging:
  level:
    root: INFO
    org.springframework.web: DEBUG

```

## 3. Run only Postgres in Docker (local app)

```yml
services:
  db:
    image: postgres:16
    container_name: customer-postgres
    environment:
      POSTGRES_DB: customerdb
      POSTGRES_USER: customer
      POSTGRES_PASSWORD: customer
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
      - ./init-scripts:/docker-entrypoint-initdb.d
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U customer -d customerdb"]
      interval: 5s
      timeout: 5s
      retries: 10

volumes:
  pgdata:
```

