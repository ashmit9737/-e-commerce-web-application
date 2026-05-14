# E-commerce Spring Boot (JSP + Hibernate)

Production-oriented Java e-commerce web application built with Spring Boot, JSP, Spring Security, and Hibernate SessionFactory.

This project follows a layered MVC architecture and supports role-based access for admin and customer workflows.

<br/><br/>

<h1>🛒 E-Commerce Spring Boot</h1>
 
<p>A production-oriented Java e-commerce web application built with Spring Boot, JSP, Spring Security, and Hibernate — featuring role-based access for admin and customer workflows.</p>
<br/>
<!-- Badges Row 1: Community -->
<br/>

## Highlights

- Server-rendered e-commerce app (JSP views)
- Spring Security authentication and role-based authorization
- Custom Hibernate SessionFactory configuration (non-Spring-Data JPA runtime)
- MySQL-backed persistence with DAO and service layers
- Admin modules for products, categories, and customer listing
- User modules for registration, login, profile management, and product browsing
- Jenkins pipeline file included for CI/CD bootstrap

## Tech Stack
- Java 11
- Spring Boot 2.6.4
- Spring MVC
- Spring Security
- Hibernate ORM (via `LocalSessionFactoryBean`)
- JSP + JSTL + Tomcat Jasper
- MySQL 8 connector
- Maven

## Project Structure

```text
src/main/java/com/jtspringproject/JtSpringProject/
  configuration/     # Security config
  controller/        # MVC controllers
  dao/               # Data access layer
  models/            # Entities
  services/          # Business layer
  repository/        # Spring Data repository (partial)
  HibernateConfiguration.java
  JtSpringProjectApplication.java
src/main/resources/
  application.properties
src/main/webapp/views/
  *.jsp
basedata.sql
pom.xml
```

## Getting Started

### Prerequisites

- Java 11+
- Maven 3.8+
- MySQL or MariaDB

### 1) Clone and move into project

```bash
git clone https://github.com/jaygajera17/E-commerce-project-springBoot.git
cd E-commerce-project-springBoot
```

### 2) Configure database

Update `src/main/resources/application.properties`:

```properties
db.driver=com.mysql.cj.jdbc.Driver
db.url=jdbc:mysql://localhost:3306/ecommjava?createDatabaseIfNotExist=true
db.username=your_db_user
db.password=your_db_password

hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
hibernate.show_sql=true
hibernate.hbm2ddl.auto=update
entitymanager.packagesToScan=com
```

### 3) Optional: seed sample data

Run `basedata.sql` against your database if you want initial categories/users/products.

Note: sample credentials in `basedata.sql` are development-only defaults.

### 4) Run the app

```bash
mvn clean package
mvn spring-boot:run
```

App URL: http://localhost:8080/

## IDE Notes (IntelliJ)

If JSP views are not resolved, set the run configuration working directory to `$MODULE_WORKING_DIR$`.

## Core Endpoints

### Public/User

- `/`
- `/login`
- `/register`
- `/newuserregister`
- `/user/products`
- `/profileDisplay`

### Admin

- `/admin/`
- `/admin/Dashboard`
- `/admin/products`
- `/admin/categories`
- `/admin/customers`

## Security Model

- Admin routes under `/admin/**` require role `ADMIN`
- User routes require role `USER`
- Login pages:
  - Admin: `/admin/login`
  - User: `/login`
- CSRF protection is enabled for form submissions

## Build and Test

```bash
mvn clean verify
```

Notes:

- `mvn test` requires a reachable database because context startup initializes Hibernate and datasource beans.

## CI/CD

A Jenkins pipeline is included in `jenkins file` with stages for:

- Checkout
- Build
- Test
- Deploy (template placeholder)

Adjust branch, deployment steps, and credentials for your environment.

## Troubleshooting

- `Could not resolve placeholder 'db.driver'`:
  - Ensure all `db.*` keys exist in `application.properties`
- JSP pages not rendering:
  - Verify working directory and `spring.mvc.view.prefix=/views/`
- Tests failing on startup:
  - Start MySQL and verify connection credentials first

