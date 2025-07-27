Absolutely — here are the **clearly written, final requirements** for your **Spring Boot REST API** using a **disk-persistent H2 database**:

---

## ✅ Objective

Create a **Spring Boot REST API** that allows clients to manage a collection of books.
Data will be stored in an **H2 database on disk** so that it persists between application restarts.

---

## 📦 Data Model: `Book`

Each book must have the following fields:

| Field      | Type      | Required             | Description                                    |
| ---------- | --------- | -------------------- | ---------------------------------------------- |
| `id`       | `long`    | Yes (auto-generated) | Unique identifier for the book                 |
| `title`    | `String`  | Yes                  | Title of the book                              |
| `author`   | `String`  | Yes                  | Author of the book                             |
| `borrowed` | `boolean` | No                   | Whether the book is borrowed (default `false`) |

### Additional rules:

* `id` is auto-generated using `@GeneratedValue`
* `equals()` and `hashCode()` must be overridden based **only on `id`**

---

## 💾 Storage Configuration

* Use **H2 database in file mode** (not in-memory)
* Example JDBC URL:
  `jdbc:h2:file:./data/bookdb`
* Data **must persist** after application restarts
* Use **Spring Data JPA** to interact with the database (no SQL needed)

---

## 🌐 REST API Endpoints

| Method   | Endpoint                 | Description           | Response Codes                           |
| -------- | ------------------------ | --------------------- | ---------------------------------------- |
| `POST`   | `/api/books`             | Add a new book        | `201 Created`, `409 Conflict` (optional) |
| `GET`    | `/api/books`             | Get all books         | `200 OK`                                 |
| `GET`    | `/api/books/{id}`        | Get book by ID        | `200 OK`, `404 Not Found`                |
| `PUT`    | `/api/books/{id}/borrow` | Mark book as borrowed | `200 OK`, `404`, `409`                   |
| `PUT`    | `/api/books/{id}/return` | Mark book as returned | `200 OK`, `404`, `409`                   |
| `DELETE` | `/api/books/{id}`        | Delete book by ID     | `200 OK`, `404 Not Found`                |

---

## 🧪 Testing

Use **Postman** to manually test the following:

* ✅ Create a book using `POST`
* ✅ Borrow a book using `PUT /borrow`
* ✅ Return a book using `PUT /return`
* ✅ Get all books with `GET`
* ✅ Get one book by `id`
* ✅ Delete a book

---

## 🔧 Optional (Bonus)

* Add default values for `title` or `author` using `@Value` from `application.properties` if not provided (not required)

