# Food Ordering System

A Spring Boot-based backend project for managing a food ordering platform. The application exposes REST APIs for customers, restaurants, menu items, orders, payments, and user registration while using JPA for database access and Spring Security for authentication.

## Overview

This project simulates a food delivery platform where:

- Customers can be created and managed
- Restaurants can register and be searched by location or rating
- Menu items can be added and priced per restaurant
- Orders can be placed, tracked, and updated
- Order items can be added or updated within a specific order
- Payments can be processed and their statuses can be monitored
- Users can register with role-based credentials for secure access

## Features

- RESTful API design using Spring MVC
- Database persistence with Spring Data JPA and Hibernate
- PostgreSQL integration
- Role-based user account support
- Basic authentication using Spring Security
- Global exception handling for invalid requests and missing resources
- Structured response format using a custom `ResponseStructure` model
- Order status and payment status management

## Tech Stack

- Java
- Spring Boot 3 / Spring Framework
- Spring Web MVC
- Spring Data JPA
- Hibernate ORM
- PostgreSQL
- Spring Security
- Maven
- Lombok

## Project Structure

```text
src/
├── main/
│   ├── java/com/springboot/FoodOrderingSystem/
│   │   ├── controller/        # REST controllers
│   │   ├── entity/            # JPA entity classes
│   │   ├── repository/        # Spring Data repositories
│   │   ├── service/           # Business logic
│   │   ├── dto/               # Response DTOs
│   │   ├── exception/         # Custom exceptions and advice
│   │   ├── security/          # Security configuration
│   │   └── FoodOrderingSystemApplication.java
│   └── resources/
│       └── application.properties
└── test/
```

## Main Modules

### 1. Customer Management
Handles customer information such as name, contact, email, and associated orders.

### 2. Restaurant Management
Supports restaurant registration, update, lookup by name/location, and retrieving restaurant menus.

### 3. Menu Management
Allows adding menu items to restaurants, updating prices and stock/availability, and fetching menu items by name or price.

### 4. Order Management
Controls the order lifecycle, including:

- placing orders
- fetching orders by customer, restaurant, date, or status
- updating order status
- cancelling an order

### 5. Order Item Management
Adds, updates, removes, and fetches items within orders.

### 6. Payment Management
Tracks payment creation, status, method, and order-based payment lookup.

### 7. User Management
Registers users and loads user details for authentication in the security layer.

## Security

This application uses Spring Security with HTTP Basic authentication.

- All HTTP requests are currently protected by default
- The project uses a custom `UserDetailsService`
- Passwords are stored and validated using a simple `NoOpPasswordEncoder`

> Note: The current configuration requires valid credentials for API access. Update this if you want a more production-ready security setup with BCrypt hashing and role-based authorization.

## Database Configuration

The application is configured to connect to PostgreSQL in `src/main/resources/application.properties`.

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/LibraryDB
spring.datasource.username=postgres
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
```

Before running the project:

1. Create a PostgreSQL database.
2. Update the database URL, username, and password to match your local setup.
3. Ensure the database server is running.

## Prerequisites

- Java 26 (as configured in the project)
- Maven
- PostgreSQL
- A local database instance

## Getting Started

### Clone the project

```bash
git clone <repository-url>
cd FoodOrderingSystem
```

### Build the project

```bash
./mvnw clean install
```

### Run the application

```bash
./mvnw spring-boot:run
```

The Spring Boot app will start on the default port:

```text
http://localhost:8080
```

## API Overview

Base path:

```text
/api
```

### User APIs

```text
POST /api/users/register
```

### Customer APIs

```text
GET    /api/customers
GET    /api/customers/{id}
POST   /api/customers
PUT    /api/customers/{id}
DELETE /api/customers/{id}
GET    /api/customers/contact/{contact}
GET    /api/customers/email/{email}
GET    /api/customers/name/{name}
```

### Restaurant APIs

```text
GET    /api/restaurants
GET    /api/restaurants/{id}
POST   /api/restaurants
PUT    /api/restaurants/{id}
DELETE /api/restaurants/{id}
GET    /api/restaurants/location/{location}
GET    /api/restaurants/name/{name}
GET    /api/restaurants/rating/{rating}
GET    /api/restaurants/{id}/menu
```

### Menu Item APIs

```text
GET    /api/menu-items
GET    /api/menu-items/{id}
POST   /api/menu-items/restaurant/{restaurantId}
PUT    /api/menu-items/{id}
GET    /api/menu-items/sort-by-price
GET    /api/menu-items/name/{name}
GET    /api/menu-items/restaurant/{restaurantId}
```

### Order APIs

```text
GET    /api/orders
GET    /api/orders/{id}
POST   /api/orders
PUT    /api/orders/{id}/status
PUT    /api/orders/{id}/cancel
GET    /api/orders/customer/{customerId}
GET    /api/orders/status/{status}
GET    /api/orders/date/{date}
GET    /api/orders/restaurant/{restaurantId}
```

### Order Item APIs

```text
POST   /api/order-items/order/{orderId}
PUT    /api/order-items/{orderItemId}/quantity
DELETE /api/order-items/{orderItemId}
GET    /api/order-items/order/{orderId}
```

### Payment APIs

```text
POST   /api/payments/order/{orderId}
GET    /api/payments/{id}
GET    /api/payments/order/{orderId}
GET    /api/payments/status/{status}
GET    /api/payments/method/{method}
PUT    /api/payments/{id}/status
```

## Example Request

Example request to fetch all restaurants:

```bash
curl -u admin:admin http://localhost:8080/api/restaurants
```

## Notes

- The project is suitable for learning REST API development with Spring Boot and JPA.
- It follows a layered architecture: controller → service → repository → database.
- The code is a strong foundation for extending into a complete production-ready food delivery platform with authentication, cart logic, ratings, delivery tracking, and admin dashboards.

## License

This project is currently intended for educational and learning purposes.

## Contributing

Contributions are welcome. You can improve:

- security hardening
- role-based authorization
- validation improvements
- Swagger/OpenAPI documentation
- testing coverage
- database schema design


