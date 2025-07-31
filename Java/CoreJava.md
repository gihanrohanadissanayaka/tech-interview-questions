### ❓ Q: Is a `catch` block always required with a `try` block in Java?

**A:**  
No. A `try` block must be followed by either a `catch` block, a `finally` block, or both.  
Using a `try` block alone is **not allowed** and will cause a **compilation error**.

---

### ✅ Valid Combinations

| Structure                  | Valid | Purpose                          |
|---------------------------|--------|----------------------------------|
| `try` only                | ❌     | Not allowed                      |
| `try` + `catch`           | ✅     | Handle exceptions                |
| `try` + `finally`         | ✅     | Always run cleanup code          |
| `try` + `catch` + `finally` | ✅   | Handle exceptions and cleanup    |

---
### ❓ Q: What is `try-with-resources` in Java?

**A:**  
`try-with-resources` is a feature introduced in **Java 7** that allows you to automatically **close resources** (like files, streams, or database connections) when you're done using them.  
It simplifies code and helps prevent resource leaks.

---
### ❓ Q: What happens if both `try` and `finally` blocks have return statements in Java?

**A:**  
When both `try` and `finally` blocks contain `return` statements, the **`return` in the `finally` block overrides the `return` in the `try` block**.

This means the value returned from the `finally` block is the one the method actually returns, and the `try` block's return value is discarded.

---

### 📄 Example:

```java
public int testMethod() {
    try {
        return 1;
    } finally {
        return 2;
    }
}
```
---
### ❓ Q: What happens if a value returned from a `try` block is modified in the `finally` block?

**A:**  
- If the `try` block returns a **primitive or immutable object**, the **value returned is fixed when the `return` statement executes**.
- The `finally` block executes **after** the `return` value is determined but **before the method actually returns**.
- **Modifying a primitive or reassigning the return variable in `finally` does NOT affect the returned value.**

---

### 📄 Example with primitive:

```java
public int testMethod() {
    int value = 1;
    try {
        return value;
    } finally {
        value = 2;  // This does NOT change the returned value
    }
}

public StringBuilder testMethod() {
    StringBuilder sb = new StringBuilder("Try");
    try {
        return sb;
    } finally {
        sb.append(" finally");  // This modifies the returned object's state
    }
}

```
---
### ❓ Q: Is nested `try-catch` possible in Java?

**A:**  
Yes, Java **allows nested `try-catch` blocks**, meaning you can put a `try-catch` inside another `try` or `catch` block.  
This is useful for handling different exceptions at different levels or scopes.

---

### 📄 Example of nested try-catch:

```java
try {
    System.out.println("Outer try block");
    
    try {
        int result = 10 / 0;  // Causes ArithmeticException
    } catch (ArithmeticException e) {
        System.out.println("Inner catch: ArithmeticException caught");
    }
    
    String str = null;
    System.out.println(str.length());  // Causes NullPointerException
} catch (NullPointerException e) {
    System.out.println("Outer catch: NullPointerException caught");
}
```
---
### ❓ Q: When will the `finally` block NOT execute in Java?

**A:**  
**If the JVM crashes or is forcibly terminated** (e.g., calling `System.exit()` inside the `try` or `catch` block):  
```java
try {
    System.exit(0);
} finally {
    // This will NOT execute
}
```
---
### ❓ Q: What is the difference between `final`, `finally`, and `finalize` in Java?
**A:**
| Term       | Type    | Purpose                                            | Usage                            |
| ---------- | ------- | ------------------------------------------------- | ------------------------------- |
| `final`    | Keyword | Declare constants, prevent override or inheritance | `final int x = 10;`              |
| `finally`  | Block   | Always execute after try/catch                     | Resource cleanup                 |
| `finalize` | Method  | Called by GC before object is collected            | Cleanup before GC removes object |
---
### ❓ Q: What happens if we add or remove elements from an `ArrayList` while iterating through it?

---

Modifying an `ArrayList` (adding/removing elements) while iterating using a standard `for` loop or an enhanced `for-each` loop can lead to **unexpected behavior** or **runtime exceptions**.`ConcurrentModificationException`

---

#### ✅ Safe ways to modify a list during iteration:

1. **Using an Iterator and its `remove()` method:**

```java
List<String> names = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));
Iterator<String> iterator = names.iterator();

while (iterator.hasNext()) {
    String name = iterator.next();
    if (name.equals("Bob")) {
        iterator.remove(); // ✅ Safe removal
    }
}
```
---
### ❓ Q: Can we use `null` in a `switch` case in Java?

#### ✅ Answer:

In **Java**, using `null` as a `switch` expression will throw a **`NullPointerException`**, **unless** you are using **Java 7+ with `String`** and handle `null` separately **before** the `switch`.
In ** Java** 21 you can use `null` as swith case.

---
### ❓ Q: Can a child class access a private method from its parent class in Java?

#### ✅ Answer:

**No**, a child class **cannot access** a `private` method of its parent class.  
`private` methods are only accessible within the same class where they are declared.

#### 🔍 Example:

```java
class Parent {
    private void showSecret() {
        System.out.println("This is private");
    }
}

class Child extends Parent {
    void reveal() {
        // showSecret(); // ❌ Compilation error: cannot find symbol
    }
}
```
---
### ❓ Why is `String` immutable in Java?

In Java, the `String` class is **immutable**, meaning once a `String` object is created, it cannot be changed. Any modification results in the creation of a **new String object**.

---

#### ✅ Reasons Why Strings Are Immutable

1. **🔐 Security**
   - Strings are used in critical areas like class loading, file paths, database URLs, and network connections.
   - If `String` were mutable, malicious code could change its value after validation, causing serious security issues.
   - Example:
     ```java
     Class.forName("com.mysql.jdbc.Driver"); // unsafe if mutable
     ```

2. **🧵 Thread Safety**
   - Immutable objects are inherently **thread-safe**.
   - Multiple threads can safely share a `String` without synchronization or data corruption.

3. **🚀 String Pooling (Performance Optimization)**
   - Java uses a **string constant pool** to store and reuse common string literals.
   - Immutability ensures that once added to the pool, the string content doesn’t change, enabling memory and performance optimization.
   - Example:
     ```java
     String a = "hello";
     String b = "hello";
     System.out.println(a == b); // true — same object from pool
     ```

4. **⚡ Hash Code Caching**
   - `String` overrides `hashCode()` and caches the value.
   - Since the value never changes, the cached hash code remains valid, improving performance in hash-based collections like `HashMap` and `HashSet`.

5. **📦 Predictable Behavior**
   - Immutable objects are easier to reason about.
   - Strings passed across methods or stored in collections won’t change unexpectedly.

---
**Tag:** #Java #Collections #Core
