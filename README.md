# 🧪 API Testing Portfolio — ReqRes & Trello

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![REST API](https://img.shields.io/badge/REST-API-blue?style=for-the-badge)
![JavaScript](https://img.shields.io/badge/JavaScript-Tests-yellow?style=for-the-badge&logo=javascript&logoColor=black)
![Status](https://img.shields.io/badge/Tests-Passing-success?style=for-the-badge)

A hands-on API testing project built with **Postman**, covering two real-world REST APIs — **ReqRes.in** and **Trello**. This project demonstrates end-to-end API testing including CRUD operations, authentication, environment variables, dynamic request chaining, and JavaScript test assertions.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Tools & Technologies](#tools--technologies)
- [APIs Tested](#apis-tested)
- [ReqRes Test Coverage](#reqres-test-coverage)
- [Trello Test Coverage](#trello-test-coverage)
- [Folder Structure](#folder-structure)
- [How to Import and Run](#how-to-import-and-run)
- [Environment Variables](#environment-variables)
- [Key Testing Techniques Used](#key-testing-techniques-used)
- [Author](#author)

---

## 📖 Project Overview

This project was built to demonstrate practical, real-world API testing skills using industry-standard tools. The testing covers:

- Full **CRUD operations** — Create, Read, Update, Delete
- **Status code validation** — 200, 204, 404
- **Response body assertions** — field existence, value matching
- **Response time checks** — performance validation
- **Environment variables** — reusable dynamic data
- **Request chaining** — auto-saving IDs between requests using pre-request and test scripts
- **Dynamic data generation** — random names generated per run to avoid conflicts
- **Error response testing** — verifying 404 for deleted resources

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| [Postman](https://www.postman.com/) | API testing, collections, environments |
| JavaScript | Test assertions and pre-request scripts |
| Postman Environments | Managing dynamic variables across requests |
| Request Chaining | Auto-passing IDs between dependent requests |
| Dynamic Variables | Random data generation using `Math.random()` |

---

## 🌐 APIs Tested

### 1. ReqRes (`https://reqres.in`)
A free hosted REST API built for testing — no authentication required. Used to test standard user CRUD operations.

### 2. Trello API (`https://api.trello.com`)
A real project management API authenticated via **API Key and Token**. Used to test a full board → list → card lifecycle with create, read, update, delete, and archive operations.

---

## ✅ ReqRes Test Coverage

| # | Request | Method | Endpoint | Test Assertions |
|---|---|---|---|---|
| 1 | Single User | GET | `/api/users/2` | Status 200, email field exists, response time < 600ms |
| 2 | List User | PUT | `/api/users/{{user_Id}}` | Response data ID equals 2 |
| 3 | List Resources | GET | `/api/unknown` | Status 200 |
| 4 | Generic Resource | GET | `/api/products` | Status 200 |
| 5 | Register Success | POST | `/api/register` | Status 200 |
| 6 | Login Success | POST | `/api/login` | Status 200 |
| 7 | Update User | PUT | `/api/users/2` | Status 200 |
| 8 | Delete User | DELETE | `/api/users/2` | Status 204 |

**Collection-level test:** Every request also runs a global assertion — response time under 3000ms.

---

## ✅ Trello Test Coverage

| # | Request | Method | What Was Tested |
|---|---|---|---|
| 1 | Create Board | POST | Status 200, board name exists, board ID saved to environment |
| 2 | Get Created Board | GET | Status 200, board ID matches environment, board not closed |
| 3 | Create List | POST | Status 200, list name matches dynamic value, not closed, list ID saved |
| 4 | Get Created List | GET | Status 200, list ID and name match environment |
| 5 | Create Card | POST | Status 200, card name matches dynamic value, card ID saved |
| 6 | Get Card | GET | Status 200, card ID matches, card belongs to correct list |
| 7 | Update Board | PUT | Status 200, name exists, board ID unchanged |
| 8 | Get Updated Board | GET | Status 200, board still exists |
| 9 | Update List | PUT | Status 200, name exists, list ID unchanged |
| 10 | Get Updated List | GET | Status 200, list ID matches environment |
| 11 | Update Card | PUT | Status 200, name exists, card ID unchanged |
| 12 | Get Updated Card | GET | Status 200, card ID matches environment |
| 13 | Delete Card | DELETE | Status 200, deletion confirmed |
| 14 | Get Deleted Card | GET | Status 404, card no longer exists, response time < 500ms |
| 15 | Archive List | PUT | Status 200, closed field exists in response |
| 16 | Get Archived List | GET | Status 200, closed = true confirmed |
| 17 | Delete Board | DELETE | Status 200, deletion confirmed |
| 18 | Get Deleted Board | GET | Status 404, board no longer exists, response time < 500ms |

---

## 📁 Folder Structure

```
API-Testing-Portfolio/
│
├── Postman/
│   ├── ReqRes_Collection.json          # Postman collection — ReqRes API
│   ├── Trello_Collection.json          # Postman collection — Trello API
│   └── Environments/
│       ├── ReqRes_environment.json     # Environment variables for ReqRes
│       └── Trello_environment.json     # Environment variables for Trello
│
└── README.md
```

---

## ▶️ How to Import and Run

### Step 1 — Import the Collection
1. Open **Postman**
2. Click **Import** (top left)
3. Select `ReqRes_Collection.json` or `Trello_Collection.json`
4. Click **Import**

### Step 2 — Import the Environment
1. Click **Environments** in the left sidebar
2. Click **Import**
3. Select `ReqRes_environment.json` or `Trello_environment.json`
4. Click **Import**

### Step 3 — Configure Environment Values

**ReqRes:**
| Variable | Value |
|---|---|
| `base_url` | `https://reqres.in` |
| `user_Id` | Leave empty — set automatically by pre-request script |

**Trello:**
| Variable | Value |
|---|---|
| `Key` | Your Trello API Key |
| `Token` | Your Trello Token |
| `base_url` | `https://api.trello.com` |
| All others | Leave empty — filled automatically by test scripts |

> ⚠️ Get your Trello API Key and Token from: https://trello.com/app-key

### Step 4 — Run the Collection
1. Click the **3 dots (...)** next to the collection name
2. Click **Run collection**
3. Make sure the correct environment is selected
4. Click **Run**

---

## 🔑 Environment Variables

### ReqRes Environment
| Variable | Type | Set By |
|---|---|---|
| `base_url` | Manual | You set this before running |
| `user_Id` | Dynamic | Pre-request script sets to `"2"` automatically |

### Trello Environment
| Variable | Type | Set By |
|---|---|---|
| `Key` | Manual | Your Trello API Key |
| `Token` | Manual | Your Trello Token |
| `base_url` | Manual | `https://api.trello.com` |
| `boardID` | Dynamic | Auto-saved by POST Create Board test script |
| `listID` | Dynamic | Auto-saved by POST Create List test script |
| `cardID` | Dynamic | Auto-saved by POST Create Card test script |
| `mylistname` | Dynamic | Auto-generated random name in pre-request script |
| `myCardName` | Dynamic | Auto-generated random name in pre-request script |

---

## 🧠 Key Testing Techniques Used

### 1. Request Chaining
IDs returned from POST requests are automatically saved and reused in subsequent requests:
```javascript
// In POST Create Board — test script
pm.environment.set("boardID", pm.response.json().id);

// Used in all following requests as {{boardID}}
```

### 2. Dynamic Data Generation
Random names are generated before each run to avoid duplicate data conflicts:
```javascript
// In Create List — pre-request script
let randomNum = Math.floor(Math.random() * 1000).toString().padStart(3, '0');
let uniqueValue = `mylist${randomNum}`;
pm.environment.set("mylistname", uniqueValue);
```

### 3. Deletion Verification
After deleting a resource, a GET request confirms it returns 404:
```javascript
pm.test("Status code is 404 - Card no longer exists", function () {
    pm.response.to.have.status(404);
});
```

### 4. Collection-Level Assertions
A global test runs on every single request in the ReqRes collection:
```javascript
pm.test("Response time is less than 3 seconds", function () {
    pm.expect(pm.response.responseTime).to.be.below(3000);
});
```

---

## 👤 Author

**Samar Shrestha**
- LinkedIn: [linkedin.com/in/your-profile](www.linkedin.com/in/samar-shrestha-512101249)
- GitHub: [github.com/Samar-Shrestha](https://github.com/Samar-Shrestha)
- Email: shresthasamar76@gmail.com

---

> 💡 *This project was built to demonstrate hands-on API testing skills using real-world APIs. Feel free to import the collections, add your own credentials, and run the tests yourself.*
