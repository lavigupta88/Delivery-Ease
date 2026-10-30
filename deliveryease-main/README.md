# DeliverEase - Delivery Management System

Java 21+ (Java 24 tested) - Spring Boot 3.5 - Spring Data JPA / Hibernate - MySQL - Spring Security + JWT - HTML/CSS/JavaScript - Maven

## Prerequisites on Any Device
1. **Java JDK 21+** (Java 21, 24, or 25)
   - Verify with: `java -version`
2. **Apache Maven 3.8+**
   - Verify with: `mvn -version`
3. **MySQL 8.0+** or **XAMPP (MySQL/MariaDB)**
   - Must be running on port `3306`.

---

## How to Run on Another Device

### 1. Database Configuration
Make sure MySQL / XAMPP is started.
In `src/main/resources/application.properties`, the settings default to:
- Port: `3306`
- Username: `root`
- Password: empty (`""`)

If your MySQL on the other device has a password (e.g. `root` or `admin`), you can either:
- **Option A (Recommended):** Set environment variables before running:
  - Windows PowerShell:
    ```powershell
    $env:SPRING_DATASOURCE_PASSWORD="your_password"
    ```
  - Linux / macOS:
    ```bash
    export SPRING_DATASOURCE_PASSWORD="your_password"
    ```
- **Option B:** Directly update `src/main/resources/application.properties`:
  ```properties
  spring.datasource.password=your_password
  ```
*(Note: Hibernate creates the `deliverease` database and all required tables automatically on startup).*

---

### 2. Run Commands

Open your terminal in the project directory (where `pom.xml` is located):

#### Windows (PowerShell / Command Prompt):
```powershell
# Navigate into the project folder
cd deliveryease-main

# Build & Run with Spring Boot plugin
mvn spring-boot:run
```

Or build a standalone JAR and run directly:
```powershell
mvn clean package -DskipTests
java -jar target/deliverease-1.0.0.jar
```

#### macOS / Linux:
```bash
cd deliveryease-main
mvn spring-boot:run
```

---

### 3. Open in Browser
- **Application URL:** [http://localhost:8080](http://localhost:8080)
- **Database Viewer (if using XAMPP):** [http://localhost/phpmyadmin/](http://localhost/phpmyadmin/)

---

## Demo Accounts (Seeded automatically on first startup)
| Role | Email | Password |
|---|---|---|
| Admin | admin@deliverease.com | admin123 |
| Delivery Partner 1 | ravi@deliverease.com | partner123 |
| Delivery Partner 2 | anita@deliverease.com | partner123 |
| Customer | Register any new account on the login screen | User chosen |

## REST API summary
| Method | Endpoint | Access |
|---|---|---|
| POST | /api/auth/register, /api/auth/login | Public |
| GET/PUT | /api/profile | Any logged-in user |
| GET | /api/track/{trackingId} | Public |
| POST | /api/orders | Customer |
| GET | /api/orders[?status=] | Admin (all) / Customer (own) / Partner (assigned) |
| PUT | /api/orders/{id}/assign?partnerId= | Admin |
| PUT | /api/orders/{id}/cancel | Customer (own) / Admin |
| PUT | /api/orders/{id}/status | Delivery Partner |
| GET/POST/PUT | /api/partners, /api/partners/{id}, /api/partners/{id}/active?value= | Admin |
| GET | /api/dashboard | Admin |
