
# SpringBatch

A Spring Boot microservice demonstrating **Spring Batch** integration with **MySQL** as a persistent job repository.

---

## 📦 Technologies

- **Java 17**
- **Spring Boot 3.x**
- **Spring Batch 5.x**
- **Spring Data JPA**
- **MySQL 8+**
- **Maven**

---

## 🧱 Project Structure

```
├── src/
│   ├── main/
│   │   ├── java/com/devbuild/
│   │   │   └── SpringBatchApplication.java
│   │   ├── resources/
│   │       ├── application.properties
│   │       └── schema-mysql.sql        # Spring Batch schema for MySQL
└── pom.xml
```

---

## ⚙️ Configuration (`application.properties`)

```properties
spring.application.name=SpringBatch

# MySQL
spring.datasource.url=jdbc:mysql://localhost:3306/spring_batch_db?useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=admin
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# Spring Batch schema initialization
spring.batch.jdbc.initialize-schema=always
spring.datasource.platform=mysql

# Server
server.port=8080
```

---

## 🚀 Setup Instructions

1. **Clone the repo**  
   ```bash
   git clone https://github.com/RupendraJaiswal/SpringBatch.git
   cd SpringBatch
   ```

2. **Create MySQL database**  
   ```sql
   CREATE DATABASE spring_batch_db;
   ```

3. **Run the Spring Batch schema** (optional if auto-initialized):  
   - Use `src/main/resources/schema-mysql.sql` to create tables.

4. **Start the application**  
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

---

## ✅ How It Works

- Spring Boot auto-configures the DataSource and Batch JobRepository.
- `spring.batch.jdbc.initialize-schema=always` initializes the batch tables (`BATCH_JOB_INSTANCE`, etc.) if they don’t exist.
- The sample job runs and logs output like:
  ```
  JobLauncher - Job: [SimpleJob: [name=...]] launched...
  Job completed with status: COMPLETED
  ```

---

## 🛠️ Troubleshooting

| Issue | Fix |
| --- | --- |
| `Unknown column CREATE_TIME` | Update schema: add `CREATE_TIME DATETIME NOT NULL` to `BATCH_STEP_EXECUTION`. |
| Driver errors | Ensure `mysql-connector-j` is in `pom.xml` and the JDBC URL is correct. |
| Tables missing | Verify `schema-mysql.sql` matches Spring Batch 5.x schema. |

---

## 🧩 `schema-mysql.sql`

Included file contains the full SQL definitions for required batch tables:

- `BATCH_JOB_INSTANCE`, `BATCH_JOB_EXECUTION`, `BATCH_JOB_EXECUTION_PARAMS`
- `BATCH_STEP_EXECUTION`, `BATCH_STEP_EXECUTION_CONTEXT`, `BATCH_JOB_EXECUTION_CONTEXT`

---

## ☁️ Next Steps

- Define your **Job**, **Step**, **ItemReader**, **Processor**, **Writer** (see `/job` or `/config` packages).
- Add Spring Profiles for different environments (dev, test, prod).
- Integrate with Spring Boot Actuator or metrics.

---

## 📝 License

MIT License. Feel free to use and customize it.

---

## © Rupendra Jaiswal

*Let's batch process things better together!* 🚀
