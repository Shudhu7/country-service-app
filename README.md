
### 🔁 Request Flow

1. **Client** sends HTTP request (GET, POST, PUT, DELETE).
2. **Controller** handles the request and delegates it to the **Service**.
3. **Service** contains the business logic and interacts with the **Repository**.
4. **Repository** performs persistence operations on the database via JPA.
5. **Bean** (Entity class) maps to a table in the **Database**.
6. HTTP response flows back to the **Client** through the same layers.

---

## 🚀 Features

- Get all countries
- Get a country by name
- Add a new country
- Update an existing country
- Delete a country

---

## 🔧 Technologies Used

- **Spring Boot**
- **Spring Data JPA**
- **Java 17+**
- **Maven**
- **MySQL (or H2 for testing)**
- **REST APIs**
- **Postman (for testing)**

---

## 📁 Project Structure

src/
└── main/
└── java/
└── com/countryservice/demo/
├── controllers/ --> API layer (Controller classes)
├── services/ --> Business logic
├── repositories/ --> Data access interfaces (Repository)
└── bean/ --> JPA Entities (Country.java, etc.)
