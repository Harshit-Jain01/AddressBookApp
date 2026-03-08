# 📒 AddressBookApp

A **Spring Boot based Java application** developed using the **Test-Driven Development (TDD)** methodology to build a structured and scalable Address Book system.

---

### 📖 Overview

- A modular Spring Boot application designed to manage Address Book contacts with structured data handling and retrieval capabilities.
- The project evolves through a sequence of incremental Use Cases, beginning with basic contact creation and gradually introducing advanced features such as searching, sorting, persistence, and database integration.
- Follows a clean layered architecture using Controller–Service–Repository components to maintain clear separation of responsibilities.
- Focuses on maintainability, testability, and scalable project structure as the application grows.

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

## 🧩 UC7 – Avoid Duplicate Contacts :
  - Improves the Address Book system by ensuring that duplicate contacts cannot be stored within the same Address Book.
  - Each contact is uniquely determined using the combination of first name and last name.

  **Purpose**
  - Preserve data accuracy by preventing repeated contact entries.
  - Ensure that the same individual cannot be added multiple times to a single Address Book.

  **Implementation**
  - Introduced validation logic in `AddressBookService` to check for existing contacts before inserting a new one.
  - Used Java Streams with the `anyMatch()` method to detect if a contact with the same `firstName` and `lastName` already exists.
  - If a duplicate is found, an exception is thrown to stop the contact from being added.
  - Added unit tests to confirm duplicate detection, successful insertion of unique contacts, and allowing identical contacts in different Address Books.

---

---
## 🧩 UC8 – Find Contacts by City or State :
  - Adds functionality to search for contacts based on city or state across all Address Books.
  - Allows filtering of contacts using their location details.

  **Purpose**
  - Help users easily locate contacts belonging to a particular city or state.
  - Enable searching across every Address Book available in the system.

  **Implementation**
  - Implemented search logic in `AddressBookService` using Java Streams.
  - Aggregated contacts from all Address Books and applied filters based on the provided city or state.
  - Added REST endpoints in `AddressBookController`:
    ```
    GET /addressbooks/search/city/{city}
    GET /addressbooks/search/state/{state}
    ```
  - Added unit tests to verify correct search results, case-insensitive comparisons, handling of multiple matches, and situations where no contacts are found.

---
## 🧩 UC9 – Display Contacts by City or State :
  - Adds the capability to view contacts organized by city or state across different Address Books.
  - Helps structure contact data based on location for better visibility.

  **Purpose**
  - Allow users to view contacts grouped according to their city or state.
  - Provide an organized way to manage and analyze contacts based on location details.

  **Implementation**
  - Implemented grouping functionality in `AddressBookService` using Java Streams with `Collectors.groupingBy()`.
  - Contacts are arranged in a map-based structure:
    ```
    Map<String, List<Contact>>
    ```
  - Added REST endpoints in `AddressBookController`:
    ```
    GET /addressbooks/view/city
    GET /addressbooks/view/state
    ```
  - Added unit tests to validate grouping behavior, support multiple Address Books, and handle cases where no contacts are present.

---
## 🧩 UC10 – Contact Count by City or State :
  - Adds functionality to calculate the number of contacts grouped by city or state across different Address Books.
  - Helps provide insights into how contacts are distributed across various locations.

  **Purpose**
  - Enable users to find out the total number of contacts present in each city or state.
  - Provide summarized contact statistics across all Address Books in the system.

  **Implementation**
  - Implemented counting logic in `AddressBookService` using Java Streams with `Collectors.groupingBy()` and `Collectors.counting()`.
  - The results are stored in the structure:
    ```
    Map<String, Long>
    ```
  - Added REST endpoints in `AddressBookController`:
    ```
    GET /addressbooks/count/city
    GET /addressbooks/count/state
    ```
  - Added unit tests to verify counting functionality across multiple Address Books, handle empty data scenarios, and validate contacts belonging to different cities or states.

---
## 🧩 UC11 – Sort Contacts Alphabetically by Name :
  - Introduces the ability to sort contacts alphabetically by their first name within an Address Book.
  - Improves usability by presenting contacts in an organized and readable order.

  **Purpose**
  - Allow users to view contacts arranged alphabetically for easier navigation.
  - Provide a consistent way to display contact lists within an Address Book.

  **Implementation**
  - Implemented sorting logic in `AddressBookService` using Java Streams and `Comparator.comparing()` based on the `firstName` field.
  - Added a REST endpoint in `AddressBookController`:
    ```
    GET /addressbooks/{bookName}/sort/name
    ```
  - Overrode the `toString()` method in the `Contact` model to produce readable output when displaying contact entries.
  - Added unit tests to validate sorting functionality, handling of empty Address Books, and multiple contacts.
    
---
## 🧩 UC12 – Sort Contacts by City, State, or Zip :
  - Enhances the system to allow contacts to be arranged by city, state, or zip code within an Address Book.
  - Provides multiple ways to organize contact information based on location details.

  **Purpose**
  - Enable users to view contacts ordered by city, state, or zip code.
  - Improve the structure and accessibility of contact data using geographical attributes.

  **Implementation**
  - Implemented sorting functionality in `AddressBookService` using Java Streams with `Comparator.comparing()` for the fields `city`, `state`, and `zip`.
  - Added REST endpoints in `AddressBookController`:
    ```
    GET /addressbooks/{bookName}/sort/city
    GET /addressbooks/{bookName}/sort/state
    GET /addressbooks/{bookName}/sort/zip
    ```
  - Added unit tests to verify sorting behavior, including cases with empty Address Books and scenarios containing a single contact.
---
## 🧩 UC13 – File I/O Integration :
  - Adds support for storing and retrieving Address Book contacts using Java File I/O.
  - Allows contacts to be written to a file and later read back into the application.

  **Purpose**
  - Enable Address Book data to be saved permanently outside the application's runtime memory.
  - Allow contacts to be restored from a saved file whenever needed.

  **Implementation**
  - Developed a helper class `FileUtil` to handle file operations using `BufferedWriter` and `BufferedReader`.
  - Implemented functionality to export contacts from an Address Book to a file and import them back into memory.
  - Added REST endpoints in `AddressBookController`:
    ```
    POST /addressbooks/{bookName}/save
    GET /addressbooks/load
    ```
  - Added unit tests to verify file creation, reading data from files, handling empty files, and persisting multiple contacts.

---
## 🧩 UC14 – CSV File Integration

Adds support for storing and retrieving Address Book contacts using a structured CSV file format.  
This feature allows exporting contacts to CSV files and importing them back into the application.

### Purpose
- Enable contacts to be saved and loaded using a structured **CSV file format**.
- Provide a **portable and standardized format** for storing contact data.

### Implementation
- Developed a utility class `CSVUtil` to handle CSV operations using the **OpenCSV** library (`CSVReader` and `CSVWriter`).
- Implemented methods to write contacts from an Address Book to a CSV file and read contacts from a CSV file into memory.
- Added REST API endpoints in `AddressBookController`:

  **POST /addressbooks/{bookName}/save-csv**  
  **GET /addressbooks/load-csv**

- Included unit tests to verify CSV file creation, reading contacts from CSV files, handling multiple contacts, and processing empty CSV files.
---
## 🧩 UC15 – JSON File Integration

Adds support for storing and retrieving Address Book contacts using a structured JSON format.  
This feature enables exporting contacts to JSON files and importing them back into the application.

### Purpose
- Allow contacts to be saved and retrieved in a **structured JSON format**.
- Provide a **flexible and widely used format** for storing and exchanging contact data.

### Implementation
- Developed a utility class `JSONUtil` to manage JSON serialization and deserialization using the **GSON** library.
- Implemented methods to write contacts from an Address Book to a JSON file and read contacts from a JSON file into memory.
- Added REST API endpoints in `AddressBookController`:

  **POST /addressbooks/{bookName}/save-json**  
  **GET /addressbooks/load-json**

- Included unit tests to verify JSON file creation, reading contacts from JSON files, handling multiple contacts, and processing empty JSON file scenarios.
---
## 🧩 UC16 – Retrieve Contacts from Database & Storage Layer Refactor

Introduces database integration to retrieve contacts using **JDBC** and refactors the storage architecture to support multiple persistence formats through a **storage abstraction layer**.

### Purpose
- Enable retrieval of contacts stored in a **relational database**.
- Decouple storage logic from business logic to allow support for **multiple storage formats** such as **File, CSV, and JSON**.

###  Implementation

- Externalized database configuration in `application.properties`, allowing Spring Boot to automatically configure a **DataSource**.
- Implemented a **ContactRepository** to execute SQL queries and map database rows to `Contact` objects.
- Added a REST API endpoint in `AddressBookController`:

---

## 🧩 UC17 – Update Contact City in Database

Adds the capability to modify a contact’s city directly in the database using JDBC through the repository layer.

###  Purpose

- Allow updating of existing contact information stored in the database.
- Demonstrate how database update operations can be performed using JDBC with Spring Boot DataSource configuration.

### ⚙️ Implementation

- Implemented an `updateContactCity()` method in **ContactRepository** that executes an SQL `UPDATE` statement using `PreparedStatement`.
- Exposed the update functionality through **AddressBookService** to handle business logic.
- Created a REST API endpoint in **AddressBookController**:

```
PUT /addressbooks/db/update-city
``` 
---
## 🧩 UC18 – Fetch Contacts Within a Date Range :
  - Extends the database querying feature to allow retrieval of contacts added within a defined date range.
  - Supports filtering contact records based on their creation date.

 ### Purpose
  - Enable users to view contacts that were added to the Address Book during a particular time interval.
  - Provide date-based filtering to improve data retrieval and analysis.

  **Implementation**
  - Introduced a `date_added` column in the database to store the creation date of each contact.
  - Updated `ContactRepository` to run a JDBC query using `PreparedStatement` that selects contacts whose `date_added` falls between two specified dates.
  - Added a REST endpoint in `AddressBookController`:
    ```
    GET /addressbooks/db/contacts-by-date
    ```
  - Added unit tests to ensure accurate database filtering and proper retrieval of contacts within the given date range.
---
### 🧩 UC19 – Get Contact Count by City or State from Database :
  - Extends the Address Book system to calculate the number of contacts stored in the database grouped by city and state.
  - Introduces a DTO layer to improve how data is transferred in API responses.

  ### Purpose
  - Enable the system to analyze how contacts are distributed across different locations.
  - Provide summarized statistics showing the number of contacts in each city or state.
  - Improve API structure by using DTO objects instead of directly exposing domain models.

  **Implementation**
  - Utilized the existing JDBC database connection and `ContactRepository` to fetch contacts from the database.
  - Implemented grouping and counting logic in the service layer using Java Streams with `groupingBy()` and `counting()`.
  - Added REST endpoints in `AddressBookController`:
  ```
  GET /addressbooks/db/count/city
  GET /addressbooks/db/count/state
  ```
- Introduced `ContactDTO` to handle API request and response data.
- Updated controller methods to return DTO objects while the service layer performs conversion between DTOs and entity models.
- Added unit tests to verify correct grouping, counting, and DTO-based API responses.
---
### 🧩 UC20 – Insert Contact into Database Using JDBC

Enhances the Address Book system to support adding new contact records directly into the database using JDBC with transactional handling.

 ### Purpose

- Allow the application to store newly created contacts permanently in the database.
- Ensure reliable database operations by using transaction management to maintain data consistency.

###  Implementation

- Extended `ContactRepository` with an SQL `INSERT` query implemented using JDBC `PreparedStatement`.
- Implemented transaction management using `setAutoCommit(false)`, `commit()`, and `rollback()` to maintain database integrity.
- Added a service method in **AddressBookService** to handle inserting contacts through the repository layer.
- Created a REST API endpoint in **AddressBookController**:
 ```
  POST /addressbooks/db/add-contact
  ```
- Added unit tests to verify successful database insertion and correct interaction with the repository layer.
---

## 🧩 **UC21 – Insert Multiple Contacts into Database Using Multithreading :**
  - Extends the Address Book system to allow multiple contacts to be inserted into the database simultaneously using multithreading.

  **Purpose**
  - Improve efficiency when adding several contacts by executing database insert operations in parallel.
  - Demonstrate the use of Java multithreading to perform concurrent database operations.

  **Implementation**
  - Created a `threads` package and added an `AddContactTask` class that implements `Runnable` to handle insertion of individual contacts.
  - Reused the existing `addContact()` method in `ContactRepository` for JDBC-based database insertion.
  - Implemented a method in `AddressBookService` that creates and manages multiple threads, where each thread inserts a single contact into the database.
  - Added a REST endpoint in `AddressBookController`:
  ```
  POST /addressbooks/db/add-multiple
  ```
- Added tests to verify that multiple contacts are inserted successfully and that all threads finish execution before the API response is returned.
---
### 🧩 UC22 – Fetch Contacts from JSON Server using REST Assured :
  - Extends the AddressBook system to obtain contact records from an external JSON server through REST API calls executed in automated test cases.

  **Purpose**
  - Allow the application to communicate with an external REST service that provides contact information.
  - Illustrate REST API testing using the **REST Assured** library.

  **Implementation**
  - Installed and configured **json-server** to act as a mock REST API using a `db.json` file containing sample contact records.
  - Launched the JSON server on **port 3000**, exposing endpoints such as:
    ```
    GET /contacts
    ```
  - Added the **REST Assured dependency** to the project to enable HTTP request handling within JUnit tests.
  - Created a test case that sends a **GET request** to the JSON server endpoint and verifies the **HTTP status code** along with the **contact data returned in the response**.
---
### UC23 – Add Contacts to JSON Server using REST Assured
  - Extends the AddressBook system to allow creation of new contact records on an external JSON server by sending REST API requests through automated tests.

  **Purpose**
  - Allow the application to insert new contact entries into a REST-based data source.
  - Demonstrate the use of REST Assured for sending POST requests and validating API responses.

  **Implementation**
  - Configured the **json-server** mock REST API running on **port 3000**, using a `db.json` file to store contact data.
  - Developed a REST Assured test that sends a **POST request** to:
    ```
    POST /contacts
    ```
  - Provided contact details in JSON format using `contentType("application/json")` along with a request body.
  - Validated the API response by checking the HTTP status **201 Created** and confirming the returned JSON data.
---
### 🧩 UC24 – Modify Contact in JSON Server using REST Assured
  - Extends the AddressBook system to allow modification of existing contact records on an external JSON server through REST API calls executed via automated tests.

  **Purpose**
  - Allow the application to update contact details stored in a REST-based data source.
  - Demonstrate how REST Assured can be used to send HTTP PUT requests and validate API responses.

  **Implementation**
  - Utilized the **json-server** mock REST API running on **port 3000**, with a `db.json` file maintaining contact records.
  - Developed a REST Assured test that sends a **PUT request** to:
    ```
    PUT /contacts/{id}
    ```
  - Provided the updated contact information in JSON format using `contentType("application/json")` along with a request body.
  - Confirmed the API response by verifying the HTTP status **200 OK** and validating the returned JSON data.
---
### 🧩 UC25 – Delete Contact from JSON Server via REST Assured :
  - Extends the AddressBook application to allow deletion of contact entries from an external JSON server using REST API requests executed through automated tests.

  **Purpose**
  - Provide the capability to remove contact data stored in a REST-based service.
  - Illustrate how REST Assured can be used to perform HTTP DELETE operations and verify the server response.

  **Implementation**
  - Utilized the **json-server** mock REST API running on **port 3000**, with contact information maintained in the `db.json` file.
  - Developed a REST Assured test case that issues a **DELETE request** to the endpoint:
    ```
    DELETE /contacts/{id}
    ```
  - Confirmed successful deletion by validating the server response with HTTP status **200 OK**.
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
│   │   │   |
│   │   │   ├── dto
│   │   │   │   └── ContactDTO.java
│   │   │   │
│   │   │   ├── model
│   │   │   │   ├── AddressBook.java
│   │   │   │   └── Contact.java
│   │   │   │
│   │   │   ├── repository
│   │   │   │   └── ContactRepository.java
│   │   │   │
│   │   │   ├── service
│   │   │   │   └── AddressBookService.java
│   │   │   │
│   │   │   ├── storage
│   │   │   │   ├── ContactStorage.java
│   │   │   │   ├── FileStorage.java
│   │   │   │   ├── CSVStorage.java
│   │   │   │   └── JSONStorage.java
│   │   │   │
│   │   │   ├── threads
│   │   │   │   ├── AddContactTask.java
│   │   │   │
│   │   │   ├── util
│   │   │   │   ├── FileUtil.java
│   │   │   │   ├── CSVUtil.java
│   │   │   │   └── JSONUtil.java
│   │   │   │
│   │   │   └── AddressBookApplication.java
│   │   │
│   │   └── resources
│   │       └── application.properties
│   │
│   └── test
│       └── java/com/addressbookapp
│           ├── AddressBookApplicationTests.java
│           ├── AddressBookServiceTest.java
|           ├── AddressBookJsonServerTest.java
│           ├── ContactRepositoryTest.java
│           └── ContactTest.java
│
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
