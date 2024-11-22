## 🚀 **RareXDB - Coming Soon!**  

We are excited to announce that **RareXDB**, a lightweight and flexible database designed for simplicity and efficiency, will be launching very soon! Stay tuned for more updates as we prepare to bring this innovative solution to developers worldwide.

### Key Features:
- **Book-Page-Line-Word Hierarchy** for seamless data management.
- **Easy Integration** into your applications.
- **Comprehensive Documentation** and tutorials to help you get started quickly.

Stay connected and be the first to explore RareDB upon its release!

**Follow us** for updates:  
- GitHub: [rocket-raki](https://github.com/rocket-raki)

---

# **RareXDB Documentation**

RareXDB is a lightweight database prototype designed for simplicity, flexibility, and intuitive usage. Inspired by a hierarchical structure, it organizes data into **Books**, **Pages**, **Lines**, and **Words**, making data management straightforward and efficient.

---

## **📚 Table of Contents**

- [Overview](#-overview)  
- [Core Concepts](#-core-concepts)  
- [Basic Syntax](#-basic-syntax)  
- [Operations](#-operations)  
  - [Activate or Create a Book](#1-activate-or-create-a-book)  
  - [Write Data](#2-write-data)  
  - [Read Data](#3-read-data)  
  - [Rewrite Data](#4-rewrite-data)  
  - [Erase/Delete Data](#5-erase-delete-data)  
- [Examples](#-examples)  
- [Error Handling](#-error-handling)  
- [Author](#-author)
---

## **🌟 Overview**

RareXDB is built on a simple hierarchy:

| **RareXDB Term** | **Equivalent Concept** | **Description**                          |
|------------------|------------------------|------------------------------------------|
| **Book**         | Database               | Top-level data container.               |
| **Page**         | Table/Collection       | Subset of a book, containing structured data. |
| **Line**         | Column/Field           | Attribute of a page.                    |
| **Word**         | Row/Value              | Actual data stored under a line.        |

### **Hierarchical Structure**  
RareXDB organizes data as:  
```plaintext
book_name: {
    page_name: {
        line1: word1,
        line2: word2
    }
};
```

---

## **🔑 Core Concepts**

- **Books:** The highest level of data storage (e.g., `college`).  
- **Pages:** A logical grouping within a book (e.g., `class`).  
- **Lines:** Attributes or columns in a page (e.g., `student_id`, `age`).  
- **Words:** Values stored within lines (e.g., `1`, `20`).  

---

## **💻 Basic Syntax**

RareXDB operations follow a simple command structure:
```plaintext
book_name.page_name.operation({parameters});
```

**Examples:**
- Activate a database:  
  ```plaintext
  college.activate;
  ```
- Write data to a page:  
  ```plaintext
  college.class.write({student_id: 1, student_name: "Raki"});
  ```
- Read all data in a page:  
  ```plaintext
  college.class.read({});
  ```

---

## **🛠️ Operations**

### **1. Activate or Create a Book**  
Switch to or create a new database (book).  

#### **Syntax**
```plaintext
book_name.activate;
```

#### **Example**
```plaintext
college.activate;
```

---

### **2. Write Data**  
Add new lines (fields) and their corresponding words (values) to a page.  

#### **Syntax**
```plaintext
book_name.page_name.write({line1: word1, line2: word2});
```

#### **Example**
```plaintext
college.class.write({student_id: 1, student_name: "Raki", age: 20});
```

#### **Result**
```plaintext
college: {
    class: {
        student_id: 1,
        student_name: "Raki",
        age: 20
    }
};
```

---

### **3. Read Data**  
Retrieve data from a page based on conditions.

#### **Syntax**
1. **Read all data in a page:**  
   ```plaintext
   book_name.page_name.read({});
   ```
2. **Read specific lines:**  
   ```plaintext
   book_name.page_name.read({line: word});
   ```
3. **Read with projection:**  
   ```plaintext
   book_name.page_name.read({}, {[line1, line2]});
   ```

#### **Examples**
- Fetch all data:  
  ```plaintext
  college.class.read({});
  ```
- Fetch specific data:  
  ```plaintext
  college.class.read({student_name: "Raki"});
  ```
- Fetch specific fields:  
  ```plaintext
  college.class.read({}, {[student_id, student_name]});
  ```

---

### **4. Rewrite Data**  
Update existing data or add new fields.

#### **Syntax**
```plaintext
book_name.page_name.rewrite({line: word}, {line_updates});
```

#### **Examples**
- Update existing data:  
  ```plaintext
  college.class.rewrite({student_id: 1}, {student_name: "Ram", age: 22});
  ```
- Add new fields:  
  ```plaintext
  college.class.rewrite({student_id: 1}, {address: "Bangalore"});
  ```

---

### **5. Erase/Delete Data**  
Remove data from a page.

#### **Syntax**
1. **Delete specific lines:**  
   ```plaintext
   book_name.page_name.erase({line: word});
   ```
2. **Delete with a condition:**  
   ```plaintext
   book_name.page_name.erase({condition}, {line: word});
   ```
3. **Delete all lines in a page:**  
   ```plaintext
   book_name.page_name.erase({});
   ```

#### **Examples**
- Delete a specific line:  
  ```plaintext
  college.class.erase({student_name: "Raki"});
  ```
- Delete all lines in a page:  
  ```plaintext
  college.class.erase({});
  ```

---

## **🔍 Examples**

### **1. Create or Switch a Database**
```plaintext
library.activate;
```

### **2. Add Data to a Page**
```plaintext
library.books.write({title: "1984", author: "George Orwell", year: 1949});
library.books.write({title: "Brave New World", author: "Aldous Huxley", year: 1932});
```

### **3. Retrieve Data**
- Fetch all books:  
  ```plaintext
  library.books.read({});
  ```
- Fetch books by a specific author:  
  ```plaintext
  library.books.read({author: "George Orwell"});
  ```

### **4. Update Data**
```plaintext
library.books.rewrite({title: "1984"}, {year: 1950});
```

### **5. Delete Data**
- Remove a specific book:  
  ```plaintext
  library.books.erase({title: "Brave New World"});
  ```
- Clear all data in the `books` page:  
  ```plaintext
  library.books.erase({});
  ```

---

## **🚨 Error Handling**

- **Database Not Activated:**  
  `Error: No active database. Use book_name.activate to activate.`  

- **Page Not Found:**  
  `Error: Page not found in the active database.`  

- **Invalid Syntax:**  
  `Error: Invalid syntax. Check the command structure.`  

- **Unknown Command:**  
  `Error: Command not recognized. Check the documentation.`  

---

## **💡 Design Philosophy**

RareXDB is designed to:
1. **Simplify** database management with intuitive commands.  
2. **Adapt** to lightweight and educational use cases.  
3. **Deliver** a hierarchical structure that enhances readability.  

---

Feel free to **clone** this project, **contribute** improvements, or **report issues** via the GitHub repository. RareXDB simplifies data storage like never before! 🚀

 ---

 # 👨‍💻 Author: **Rakesh D**  

### 🔹 **Role**: Full Stack Python Developer & Database Architect  
### 🔹 **Affiliation**: Founder, RareXtechiez, Rare Syntax

---

### 📫 **Contact Information**  
- **Email**: [rakeshd992002@gmail.com](mailto:rakeshd992002@gmail.com)  
- **GitHub**: [rocket-raki](https://github.com/rocket-raki)  
- **LinkedIn**: [Rakesh D Reddy](https://www.linkedin.com/in/rakesh-d-reddy)
- **Website**: [RareSyntax](https://rocket-raki.github.io/raresyntax)

---

### 🛠️ **Key Contributions**  
- **RareLang**: Designed a custom programming language focused on **simplicity** and **efficiency** for database querying.  
- **RareXDB**: Developed **RareXDB**, a lightweight, flexible database with a **book-page-line-word** hierarchy for streamlined data management.  
- **Documentation**: Authored in-depth **documentation** and **tutorials** to empower developers using RareXDB and RareXLang.  

---

### 💡 **Expertise & Skills**  
- **Languages**: Python, JavaScript, SQL, NoSQL, RareXLang  
- **Technologies**: Django, Flask, Full-stack Development, Database Architecture, Thunder 
- **Specializations**: Programming Language Design, Datsbase Management SystemDesign, Technical Writing  

---

### 👥 **Collaborations & Credits**  
- Worked closely with the **RareXtechiez** team for testing, debugging, and performance enhancements.  
- Inspired by **NoSQL/RDBMS/OODBM** for database simplicity and **custom scripting languages** for unique query handling.
