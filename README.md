# DemoQA Book Store — API Testing Project

A hands-on **API Functional Testing project** for the DemoQA Book Store application using **Postman**.

The project covers REST API testing, authentication, request chaining, positive and negative testing, response validation, and performance testing.

---

## 📌 Project Overview

The objective of this project was to validate the functionality, reliability, authentication, and performance of the DemoQA Book Store APIs.


## 🌐 Application & API

**Web Application:**
https://demoqa.com/books

**API Documentation:**
https://demoqa.com/swagger/

**API Base URL:**

```text
https://demoqa.com
```

> Note: The Swagger documentation page was observed to display a blank/white screen during testing. The APIs were therefore tested directly using their documented endpoint structure.

---

# 🧪 API Endpoints Tested

| Method | Endpoint                    | Description                        | Authentication |
| ------ | --------------------------- | ---------------------------------- | -------------- |
| POST   | `/Account/v1/User`          | Create User                        | No             |
| POST   | `/Account/v1/GenerateToken` | Generate Authentication Token      | No             |
| POST   | `/Account/v1/Authorized`    | Validate User Authorization        | No             |
| GET    | `/BookStore/v1/Books`       | Retrieve All Books                 | No             |
| GET    | `/Account/v1/User/{userId}` | Retrieve User Details & Collection | Yes            |
| POST   | `/BookStore/v1/Books`       | Add Book to User Collection        | Yes            |
| DELETE | `/BookStore/v1/Book`        | Delete Book from User Collection   | Yes            |

---

# 🔐 Authentication

The project uses **Bearer Token authentication** for protected endpoints.

The authentication flow is:

```text
Create User
     ↓
Generate Token
     ↓
Store Token
     ↓
Get Books
     ↓
Store ISBN
     ↓
Add Book
     ↓
Verify User Collection
     ↓
Delete Book
     ↓
Verify Deletion
```

The JWT token is stored as a Postman environment variable and reused in subsequent authenticated requests.

# 🔗 Request Chaining

Postman environment variables were used to pass data between requests.

| Variable   | Source                  | Purpose                |
| ---------- | ----------------------- | ---------------------- |
| `baseUrl`  | Environment             | API base URL           |
| `username` | Create User             | Dynamic username       |
| `password` | Environment             | Test password          |
| `userId`   | Create User response    | Identify test user     |
| `token`    | Generate Token response | Authentication         |
| `isbn`     | Get Books response      | Identify selected book |

### Example — Store User ID

```javascript
const response = pm.response.json();

pm.environment.set("userId", response.userID);
```

### Example — Store Token

```javascript
const response = pm.response.json();

pm.environment.set("token", response.token);
```

### Example — Store ISBN

```javascript
const response = pm.response.json();

pm.environment.set("isbn", response.books[0].isbn);
```

This allows the entire API workflow to be executed without manually copying values between requests.

---

# ✅ Functional Testing

The following validations were performed using Postman.

### Response Validation

* HTTP status code validation
* Response body validation
* JSON structure validation
* Response header validation
* Authentication validation
* Response time validation
* Positive test scenarios
* Negative test scenarios

### Response Time Validation

Each applicable request was validated against a response-time requirement of less than **1000 ms**.

Example:

```javascript
pm.test("Response time is less than 1000 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

---

# 🧪 Test Scenarios

## Positive Test Cases

| Test ID | Scenario                              | Expected Result                |
| ------- | ------------------------------------- | ------------------------------ |
| API-001 | Create user with valid data           | User created successfully      |
| API-002 | Generate token with valid credentials | Token generated                |
| API-003 | Retrieve all books                    | Book list returned             |
| API-004 | Add valid book to collection          | Book added successfully        |
| API-005 | Retrieve user's book collection       | Added book displayed           |
| API-006 | Delete existing book                  | Book deleted successfully      |
| API-007 | Verify deleted book                   | Deleted book no longer appears |

## Negative Test Cases

| Test ID | Scenario                      | Expected Result           |
| ------- | ----------------------------- | ------------------------- |
| API-008 | Create duplicate user         | Request rejected          |
| API-009 | Login with wrong password     | Authentication rejected   |
| API-010 | Add book without token        | `401 Unauthorized`        |
| API-011 | Add book with invalid user ID | Request rejected          |
| API-012 | Delete non-existing book      | Request rejected          |
| API-013 | Invalid ISBN                  | Request rejected          |
| API-014 | Missing required request data | Validation error returned |

---

# 📊 Postman Test Assertions

Example status-code validation:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

Example response-header validation:

```javascript
pm.test("Content-Type is JSON", function () {
    pm.expect(pm.response.headers.get("Content-Type"))
        .to.include("application/json");
});
```

Example response-time validation:

```javascript
pm.test("Response time is below 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

Example response-body validation:

```javascript
pm.test("Response contains books", function () {
    const response = pm.response.json();
    pm.expect(response.books).to.be.an("array");
});
```

---

```text
DemoQA-API-Testing/
│
├── Postman/
│   ├── DemoQA_API_Collection.json
│   └── DemoQA_Environment.json
│
├── Test-Cases/
│   └── API_Test_Cases.xlsx
└── README.md
```

---

# 🛠️ Tools & Technologies

* **Postman** — API functional testing
* **JavaScript** — Postman test scripts
* **REST API** — API testing
* **JSON** — Request/response validation
* **Excel** — Test case and execution documentation

---

# 🔍 Key Testing Areas

### Functional Testing

* User creation
* Authentication
* Book retrieval
* Book addition
* Book deletion
* User collection verification

### Authentication Testing

* Valid token
* Missing token
* Invalid credentials
* Invalid user ID

### Data Validation

* Status codes
* Response headers
* JSON response structure
* Required fields
* Invalid data

---

# 🎯 Learning Outcomes

Through this project, I gained practical experience in:

* Designing API test scenarios
* Testing REST APIs using Postman
* Working with authentication and JWT tokens
* Creating reusable environment variables
* Implementing API request chaining
* Writing JavaScript assertions in Postman
* Performing positive and negative API testing
* Validating API response time
* Preparing professional QA test documentation

---

# 📌 Conclusion

This project demonstrates an end-to-end API testing workflow covering **functional testing**.


## 👨‍💻 Author

**Md Ashraful Islam**

Software Quality Assurance Professional

**Skills demonstrated:**
Manual Testing | API Testing | Postman | JMeter | Selenium | Playwright | Jira | JavaScript | REST API | Performance Testing

