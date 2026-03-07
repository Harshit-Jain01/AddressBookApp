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
## 🧩 UC3 – Update Existing Contact

Adds the functionality to **update an existing contact** in the Address Book through a REST API.  
This feature allows modification of stored contact details while keeping the contact record intact in the Address Book.

### Purpose

- Enable users to update contact information such as **address, city, state, zip code, phone number, and email**.
- Provide a way to **identify a contact using the first name and last name** within a specific Address Book.

### Implementation

- Implemented an **`updateContact()` method** in `AddressBookService` to locate a contact using **firstName and lastName** and update the required details.
- Created a **REST endpoint** in `AddressBookController`:

--- 
## 🧩 UC4 – Delete Contact :
  - Adds the capability to delete an existing contact from an Address Book through a REST API.
  - Allows users to manage stored contacts by removing entries when they are no longer needed.

  **Purpose**
  - Provide users the ability to remove a contact from an Address Book using the person's first name and last name.
  - Ensure that contact information remains accurate and updated within the system.

  **Implementation**
  - Created a `deleteContact()` method in `AddressBookService` to search and delete a contact from the `List<Contact>` using the `removeIf()` method.
  - Implemented a REST endpoint in `AddressBookController`:
    ```
    DELETE /addressbooks/{bookName}/contacts
    ```
  - The endpoint receives `firstName` and `lastName` as query parameters to locate the contact that needs to be removed.
  - Added unit tests to validate successful deletion, handle cases where the contact does not exist, and situations where the specified Address Book is not available.

---
## 🧩 UC5 – Support Multiple Contacts :
  - Enhances the Address Book so it can store and manage multiple contacts using Java collections.
  - Allows fetching all contacts that belong to a particular Address Book.

  **Purpose**
  - Enable the Address Book to maintain several contact records instead of only one.
  - Provide an API that returns all contacts stored in a selected Address Book.

  **Implementation**
  - Used `List<Contact>` within the `AddressBook` model to store multiple contact entries.
  - Created a `getContacts()` method in `AddressBookService` to return the list of contacts for a specified Address Book.
  - Implemented a REST endpoint in `AddressBookController`:
    ```
    GET /addressbooks/{bookName}/contacts
    ```
  - Added unit tests to check scenarios such as multiple contacts, empty contact lists, duplicate contacts, large datasets, and handling of multiple Address Books.

---
## 🧩 UC6 – Manage Multiple Address Books :
  - Enhances the application to handle several Address Books at the same time.
  - Every Address Book is identified by a unique name and operates independently.

  **Purpose**
  - Enable users to organize contacts into different Address Books such as personal, work, or family.
  - Ensure that contacts remain separate within their respective Address Books.

  **Implementation**
  - Updated the service layer to store Address Books using a `Map<String, AddressBook>` data structure.
  - Implemented service methods to create a new Address Book and fetch existing Address Books.
  - Added REST endpoints in `AddressBookController`:
    ```
    POST /addressbooks/{name}
    GET /addressbooks
    ```
  - Added unit tests to validate creation of multiple Address Books, avoid duplicate Address Book creation, and ensure proper separation of contacts between Address Books.

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
