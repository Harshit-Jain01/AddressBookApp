# 📒 AddressBookApp

A **Spring Boot based Java application** developed using the **Test-Driven Development (TDD)** methodology to build a structured and scalable Address Book system.

---

## 🧩 UC1 – Create Contact

This use case introduces the **Contact domain model**, which represents a single entry in the Address Book.

### Fields
- First Name
- Last Name
- Address
- City
- State
- Zip
- Phone Number
- Email

### Implementation
- Implemented a **Contact model class** inside the `model` package.
- All contact attributes are encapsulated using constructors and getter methods.
- Added a **JUnit test (`ContactTest`)** to ensure that Contact objects are created correctly.

---
### 📂 Project Structure
```
AddressBookApp
│
├── src
│   ├── main
│   │   └── java/com/addressbook
│   │       ├── model
│   │       │   └── Contact.java
│   │       └── AddressBookApplication.java
│   │
│   └── test
│       └── java/com/addressbook
│           └── ContactTest.java
│           └── AddressBookApplicationTests.java
├── pom.xml
└── README.md
```

## 🧰 Tech Stack
- Java 17+
- Spring Boot
- Maven
- JUnit 5
- Mockito

---

## ▶️ Run Project

```bash
./mvnw clean install
./mvnw test
./mvnw spring-boot:run

```

## ⚙️ Development Approach

This project is built using the **Test-Driven Development (TDD)** practice to maintain dependable and well-structured code.

The development process follows these stages:

1. **Create Tests First**  
   Begin by writing unit tests that define how the feature should behave before implementing the actual functionality.

2. **Write the Implementation**  
   Develop the minimum amount of code necessary so that the previously written tests pass successfully.

3. **Improve the Code (Refactoring)**  
   Enhance the code’s structure, readability, and design while ensuring that all tests still pass.

Following this continuous cycle helps maintain **code quality, reliability, and scalability** as the Address Book application evolves with new features.
