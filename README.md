# 🧠 Tech Interview Questions & Study Guide

This repository contains categorized technical interview questions with concise answers and tags. It covers topics from Java, JavaScript, Oracle SQL, Microservices, and System Design. Ideal for revision before interviews or building technical depth over time.

---

## 📁 Sections

- [Java](./Java/CoreJava.md)
- [JavaScript](./JavaScript/ES6_Basics.md)
- [Oracle SQL](./Oracle/SQL_Basics.md)
- [Microservices](./Microservices/Basics.md)
- [System Design](./SystemDesign/HighLevelDesign.md)
- [Others](./Others/Git.md)

---

## 🧾 Sample Questions

### 🔹 Java

**Q:** What is the difference between `==` and `.equals()` in Java?  
**A:**  
- `==` compares object references (memory address).  
- `.equals()` compares actual values inside objects (unless overridden defaults to reference comparison).

**Tags:** `#Java` `#ObjectComparison`

---

**Q:** What is a checked vs unchecked exception?  
**A:**  
- Checked exceptions are checked at compile-time (e.g., `IOException`).  
- Unchecked exceptions occur at runtime (e.g., `NullPointerException`).

**Tags:** `#Java` `#Exceptions`

---

### 🔹 JavaScript

**Q:** What is the difference between `var`, `let`, and `const`?  
**A:**  
- `var`: function-scoped, hoisted.  
- `let`: block-scoped, not hoisted.  
- `const`: block-scoped, can't be reassigned.

**Tags:** `#JavaScript` `#Variables` `#ES6`

---

### 🔹 SQL (Oracle)

**Q:** What is the difference between `WHERE` and `HAVING` clauses?  
**A:**  
- `WHERE` filters rows before grouping.  
- `HAVING` filters after grouping.

**Tags:** `#SQL` `#Oracle` `#Clauses`

---

### 🔹 Microservices

**Q:** What is circuit breaker pattern in microservices?  
**A:**  
A pattern to prevent cascading failure by cutting off the call to a failing service after a threshold is reached (e.g., using Resilience4J, Hystrix).

**Tags:** `#Microservices` `#DesignPattern`

---

## ✨ How to Use This Repo

- Browse the section folders for topic-wise interview questions.
- Practice and revise regularly.
- Contribute with PRs if you want to add more!

---

## 👨‍💻 Author

[Gihan Dissanayaka](https://github.com/yourusername)

---

## ⭐ Star the Repo if You Find It Helpful!
