# Spring Boot REST Country Service

A RESTful web service built with Spring Boot that provides CRUD operations for managing country data. This service allows you to create, read, update, and delete country information including country names and their capitals.

## Features

- **GET** all countries
- **GET** country by ID
- **GET** country by name
- **POST** add new country
- **PUT** update existing country
- **DELETE** remove country

## Technology Stack

- **Java 21**
- **Spring Boot 3.5.3**
- **Spring Data JPA**
- **MySQL Database**
- **Maven** for dependency management

## Prerequisites

Before running this application, make sure you have:

- Java 21 or higher installed
- MySQL server running
- Maven 3.6+ (or use the included Maven wrapper)

## Database Setup

1. Install and start MySQL server
2. Create a database named `mydb`:
   ```sql
   CREATE DATABASE mydb;
   ```
3. Update the database credentials in `src/main/resources/application.properties` if needed:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/mydb
   spring.datasource.username=root
   spring.datasource.password=password
   ```

## Installation & Running

### Using Maven Wrapper (Recommended)

1. Clone the repository
2. Navigate to the project directory
3. Run the application:
   ```bash
   # On Linux/Mac
   ./mvnw spring-boot:run
   
   # On Windows
   mvnw.cmd spring-boot:run
   ```

### Using Maven

1. Clone the repository
2. Navigate to the project directory
3. Install dependencies and run:
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

The application will start on `http://localhost:8080`

## API Endpoints

### Get All Countries
```http
GET /getcountries
```
**Response:** List of all countries

### Get Country by ID
```http
GET /getcountries/{id}
```
**Parameters:**
- `id` (path parameter) - Country ID

**Response:** Country object or 404 if not found

### Get Country by Name
```http
GET /getcountries/countryName?name={countryName}
```
**Parameters:**
- `name` (query parameter) - Country name

**Response:** Country object or 404 if not found

### Add New Country
```http
POST /addCountry
```
**Request Body:**
```json
{
    "countryName": "India",
    "countryCapital": "New Delhi"
}
```
**Response:** Created country object with auto-generated ID

### Update Country
```http
PUT /updatecountry/{id}
```
**Parameters:**
- `id` (path parameter) - Country ID to update

**Request Body:**
```json
{
    "countryName": "Updated Country Name",
    "countryCapital": "Updated Capital"
}
```
**Response:** Updated country object or 409 if conflict

### Delete Country
```http
DELETE /deletecountry/{id}
```
**Parameters:**
- `id` (path parameter) - Country ID to delete

**Response:**
```json
{
    "msg": "Country Deleted !",
    "id": 1
}
```

## Data Model

### Country Entity
```java
{
    "id": 1,
    "countryName": "India",
    "countryCapital": "New Delhi"
}
```

**Fields:**
- `id` (Integer) - Auto-generated unique identifier
- `countryName` (String) - Name of the country
- `countryCapital` (String) - Capital city of the country

## Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/countryservice/demo/
│   │       ├── SpringBootRestCountryServiceProjectApplication.java
│   │       ├── bean/
│   │       │   └── Country.java
│   │       ├── controllers/
│   │       │   ├── CountryController.java
│   │       │   └── AddResponse.java
│   │       ├── repositories/
│   │       │   └── CountryRepository.java
│   │       └── services/
│   │           └── CountryService.java
│   └── resources/
│       └── application.properties
└── test/
    └── java/
        └── com/countryservice/demo/
            └── SpringBootRestCountryServiceProjectApplicationTests.java
```

## Configuration

The application can be configured through `application.properties`:

```properties
# Application name
spring.application.name=SpringBootRestCountryServiceProject

# Database configuration
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=12345
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.generate-ddl=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

## Testing

Run the tests using:
```bash
# Using Maven wrapper
./mvnw test

# Using Maven
mvn test
```

## Example Usage

### Adding a Country
```bash
curl -X POST http://localhost:8080/addCountry \
  -H "Content-Type: application/json" \
  -d '{
    "countryName": "France",
    "countryCapital": "Paris"
  }'
```

### Getting All Countries
```bash
curl http://localhost:8080/getcountries
```

### Getting Country by ID
```bash
curl http://localhost:8080/getcountries/1
```

### Getting Country by Name
```bash
curl "http://localhost:8080/getcountries/countryName?name=France"
```

### Updating a Country
```bash
curl -X PUT http://localhost:8080/updatecountry/1 \
  -H "Content-Type: application/json" \
  -d '{
    "countryName": "Updated France",
    "countryCapital": "Updated Paris"
  }'
```

### Deleting a Country
```bash
curl -X DELETE http://localhost:8080/deletecountry/1
```

## Known Issues

- The `getCountrybyName` method in the service has a logical error in the comparison (missing return statement)
- ID generation is basic and may cause issues in concurrent environments

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

For support and questions, please open an issue in the GitHub repository.
