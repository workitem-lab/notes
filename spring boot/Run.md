### Run your Spring Boot app:

```Bash
./mvnw spring-boot:run
```


### Docker

**start**:
From the same folder where your `docker-compose.yml` lives:

```code
docker compose up -d
```

**Result:**
✅ Your Postgres container is running again
✅ Your app container (if defined) is running 
✅ pgAdmin (if defined) is running 
✅ Your data is still there

**Verify everything is running**

```
docker ps
```

You should see something like:
- customer-postgres (Up)
- customer-service (Up)
- pgadmin (Up)

**Connect to Postgres again (inside Docker)**

```
docker exec -it customer-postgres psql -U customer -d customerdb
```

**List all tables**

```
\dt
```

**Describe a table (schema, indexes, constraints)**

```
\d customers
```

stopping everything with `docker stop $(docker ps -q)` **and** `docker compose down` simply shut your containers and removed the Com


