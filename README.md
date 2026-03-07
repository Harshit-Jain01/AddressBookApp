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
## 🧩 UC2 – Add New Contact to Address Book

Introduces the capability to insert a new contact into the Address Book.  
This use case demonstrates how Object-Oriented Programming is used to manage the relationship between the **AddressBook** and **ContactPerson** classes.

### Purpose

- Allow the system to store contact details inside the Address Book.
- Demonstrate how contacts are organized and maintained within the Address Book.
- Apply Object-Oriented principles to manage the association between AddressBook and ContactPerson.

### Implementation

- Created a **ContactPerson class** to represent an individual contact with attributes such as first name, last name, address, city, state, zip, phone number, and email.
- Implemented an **AddressBook class** that maintains a collection of contacts.
- Used **List<ContactPerson>** to store multiple contacts in the Address Book.
- Implemented functionality to add new contacts through the **AddressBookMain class using console input**.
- Ensured proper interaction between AddressBook and ContactPerson using Object-Oriented concepts.

---  
### 📂 Project Structure

```
AddressBookApp
│
├── src
│   ├── main
│   │   ├── java/com/addressbookapp
│   │   │   ├── controller
│   │   │   │   └── AddressBookController.java
│   │   │   │
│   │   │   ├── model
│   │   │   │   ├── AddressBook.java
│   │   │   │   └── Contact.java
│   │   │   │
│   │   │   ├── service
│   │   │   │   └── AddressBookService.java
│   │   │   │
│   │   │   └── AddressBookApplication.java
│   │   │
│   │   └── resources
│   │       └── application.properties
│   │
│   └── test
│       └── java/com/addressbookapp
│           ├── AddressBookServiceTest.java
│           ├── AddressbookappApplicationTests.java
│           └── ContactTest.java
│── pom.xml
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
