
---

# **RareDB Documentation**  

RareDB is a database prototype designed for simplicity and flexibility. It organizes data hierarchically, inspired by the structure of books, pages, lines, and words.

---

## **RareDB Structure**

| **RareDB Term** | **Equivalent Concept** | **Description**                       |
|------------------|------------------------|---------------------------------------|
| **Book**         | Database               | The highest level of data organization. |
| **Page**         | Table/Collection       | A subset of the book containing structured data. |
| **Line**         | Column/Field           | An attribute within a page. |
| **Word**         | Row/Value              | The actual data stored under a line. |

### **Data Structure**  
```plaintext
book_name: {
    page_name: {
        line1: word1,
        line2: word2
    }
};
```

---

## **Core Operations**

### **1. Activate or Create a Book**
Switch to or create a book (database).  
```plaintext
book_name.activate
```
- If the specified book does not exist, it will be created automatically.  
- Activates the book for subsequent operations.

**Example:**  
```plaintext
college.activate
```

---

### **2. Write (Create) Data**

#### **Insert Lines into a Page**
Adds one or more lines (keys) and corresponding words (values) into a page.  
```plaintext
book_name.page_name.write({line1: word1, line2: word2});
```
- If the **page** does not exist, it will be created automatically.  

**Example:**  
```plaintext
college.class.write({student_id: 1, student_name: "Raki", age: 20});
```

**Result:**  
```plaintext
college: {
    class: {
        student_id: 1,
        student_name: "Raki",
        age: 20
    }
};
```

**Note:**  
Using the `write` command will automatically create the page if it does not already exist. For example:  
```plaintext
college.class.write({line1: "Example"});
```
This will create the `class` page inside the `college` book, if it does not already exist.

---

### **3. Read Data**

#### **Read All Lines in a Page**
Retrieves all lines and their corresponding words.  
```plaintext
book_name.page_name.read({});
```

#### **Read Specific Lines**
Fetches lines that match a given condition.  
```plaintext
book_name.page_name.read({line: word});
```

#### **Read Lines with Condition**
Filters lines using conditions and retrieves the matching data.  
```plaintext
book_name.page_name.read({condition}, {line1: word1});
```

#### **Read with Projection**
Limits the fields (lines) retrieved to specific ones.  
```plaintext
book_name.page_name.read({line: {condition: word}}, {[line1, line2]});
```

**Examples:**  
1. **Read all lines:**  
   ```plaintext
   college.class.read({});
   ```
2. **Read specific line:**  
   ```plaintext
   college.class.read({student_name: "Raki"});
   ```
3. **Read with projection:**  
   ```plaintext
   college.class.read({}, {[student_id, student_name]});
   ```

---

### **4. Rewrite (Update) Data**

#### **Update Existing Lines**
Modifies data for specific lines based on a primary key or condition.  
```plaintext
book_name.page_name.rewrite({line selection primary key}, {update words});
```

**Example:**  
```plaintext
college.class.rewrite({student_id: 1}, {student_name: "Ram", age: 22});
```

#### **Update or Create Lines**
If the specified lines do not exist, they will be created.  
```plaintext
book_name.page_name.rewrite({line selection primary key}, {update words, additional fields});
```

**Example:**  
```plaintext
college.class.rewrite({student_id: 1}, {student_name: "Ram", age: 22, address: "Bangalore"});
```

---

### **5. Erase (Delete) Data**

#### **Delete Lines with a Condition**
This operation deletes lines (columns) that match a specific condition. It is useful when you want to delete data based on specific criteria.

```plaintext
book_name.page_name.erase({condition}, {line: word});
```

- **Example:**  
```plaintext
college.class.erase({student_id: 1}, {student_name: "Raki"});
```

This will delete the line (column) where the **student_id** is `1` and the **student_name** is `"Raki"`.

#### **Delete a Specific Line**
This operation deletes a single line (row) based on its word (value). If you want to delete a specific row based on a line and word, use this format.

```plaintext
book_name.page_name.erase({line1: word1});
```

- **Example:**  
```plaintext
college.class.erase({student_name: "Raki"});
```

This will delete the line where the **student_name** is `"Raki"`.

#### **Delete All Lines in a Page**
If you want to clear all the data in a page, you can erase all lines. This will remove all the rows in that page.

```plaintext
book_name.page_name.erase({});
```

- **Example:**  
```plaintext
college.class.erase({});
```

This will remove all the lines (rows) from the **class** page in the **college** book.

---

### **Examples of Erase/Delete Operations:**

1. **Delete with a condition:**  
   This example deletes the record where **student_id** is `1` and the **student_name** is `"Raki"`.  
   ```plaintext
   college.class.erase({student_id: 1}, {student_name: "Raki"});
   ```

2. **Delete a specific line (based on word):**  
   This example deletes the record where the **student_name** is `"Raki"`.  
   ```plaintext
   college.class.erase({student_name: "Raki"});
   ```

3. **Delete all lines in a page:**  
   This example deletes all lines (data) in the **class** page.  
   ```plaintext
   college.class.erase({});
   ```

---

### **Error Handling in Erase/Delete**

1. **Line Not Found:**  
   - **Error:** `Line not found. Unable to delete.`
   - **Description:** The specified line or condition does not match any data in the page.

2. **Invalid Syntax:**  
   - **Error:** `Invalid syntax in erase/delete operation.`
   - **Description:** There is an issue with the syntax of the erase/delete command.

---

## **Examples: Full Workflow**

### **1. Create or Switch a Database**  
```plaintext
library.activate;
```

### **2. Write Data**  
```plaintext
library.books.write({title: "1984", author: "George Orwell", year: 1949});
library.books.write({title: "Brave New World", author: "Aldous Huxley", year: 1932});
```

### **3. Read Data**  
1. **Read all lines:**  
   ```plaintext
   library.books.read({});
   ```
2. **Read specific line:**  
   ```plaintext
   library.books.read({title: "1984"});
   ```
3. **Read with projection:**  
   ```plaintext
   library.books.read({}, {[title, author]});
   ```

### **4. Rewrite Data**  
1. **Update existing lines:**  
   ```plaintext
   library.books.rewrite({title: "1984"}, {year: 1950});
   ```
2. **Update and add new fields:**  
   ```plaintext
   library.books.rewrite({title: "1984"}, {publisher: "Secker & Warburg"});
   ```

### **5. Delete Data**  
1. **Delete a specific line:**  
   ```plaintext
   library.books.erase({title: "Brave New World"});
   ```
2. **Delete all lines in a page:**  
   ```plaintext
   library.books.erase({});
   ```

---

## **Error Handling**

1. **Database Not Activated:**  
   - **Error:** `No active database. Use book_name.activate to activate.`  

2. **Page Not Found:**  
   - **Error:** `Page not found in the active database.`  

3. **Invalid Syntax:**  
   - **Error:** `Invalid syntax. Check the command structure.`  

4. **Unknown Command:**  
   - **Error:** `Command not recognized. Check the documentation.`  

---

## **Design Philosophy**

RareDB aims to provide:  
1. **Simplicity:** Straightforward commands for common database tasks.  
2. **Flexibility:** Adaptable to various scenarios.  
3. **Readability:** A hierarchical structure that's easy to understand.  

**Ideal Use Cases:**  
- Lightweight applications.  
- Educational projects.  
- Quick data storage prototypes.  

---

RareDB simplifies database management with an innovative, user-friendly approach.
