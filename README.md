# mongodb-tasks
Practice repository for MongoDB CRUD operations, including basic data types, nested objects, arrays, and upsert examples.
Absolutely! I’ve taken your MongoDB tasks and formatted them neatly in **Markdown** with proper code blocks, explanations, and step-wise outputs. Here’s the complete representation:

---

# **MongoDB Practice – Tasks Completed**

## **TASK 1: Introductory Collection**

**Database:** `learning_mongo`
**Collection:** `intro_test`

### **1. Insert Documents**

```javascript
// Document with all basic data types
db.intro_test.insertOne({
    name: "Akshay",
    age: 20,
    isGraduate: true,
    date: Date(),
    subjects: ["Python", "HTML", "CSS"],
    Data: {},
    FailedSubjects: null
});

// Document with nested object
db.intro_test.insertOne({
    username: "akshay",
    age: 20,
    isGraduate: true,
    profile: {
        subjects: ["Python", "HTML", "CSS"],
        address: {
            room_no: 404,
            apartment_name: "ABC",
            street: "xyz",
            city: "Mumbai"
        }
    }
});

// Document with array of objects
db.intro_test.insertOne({
    name: "Rajesh",
    skills: [
        { skill: "Python", level: "Advanced" },
        { skill: "Data Analysis", level: "Intermediate" }
    ]
});
```

### **2. Retrieve All Documents**

```javascript
db.intro_test.find()
```

**Output Example:**

```json
[
  {
    "_id": ObjectId("..."),
    "name": "Akshay",
    "age": 20,
    "isGraduate": true,
    "date": ISODate("2025-09-08T12:00:00Z"),
    "subjects": ["Python", "HTML", "CSS"],
    "Data": {},
    "FailedSubjects": null
  },
  {
    "_id": ObjectId("..."),
    "username": "akshay",
    "age": 20,
    "isGraduate": true,
    "profile": {
      "subjects": ["Python", "HTML", "CSS"],
      "address": {
        "room_no": 404,
        "apartment_name": "ABC",
        "street": "xyz",
        "city": "Mumbai"
      }
    }
  },
  {
    "_id": ObjectId("..."),
    "name": "Rajesh",
    "skills": [
      { "skill": "Python", "level": "Advanced" },
      { "skill": "Data Analysis", "level": "Intermediate" }
    ]
  }
]
```

---

## **TASK 2: CRUD Operations on `students` Collection**

**Database:** `learning_mongo`
**Collection:** `students`

---

### **1. Create (Insert Multiple Students)**

```javascript
db.students.insertMany([
  {
    name: "sahil",
    age: 19,
    city: "Pune",
    subjects: ["HTML", "CSS"],
    profile: { grade: "A", attendance: 95 }
  },
  {
    name: "Raj",
    age: 26,
    city: "Satara",
    subjects: ["Javascript", "Math"],
    profile: { grade: "A", attendance: 98 }
  },
  {
    name: "Suraj",
    age: 22,
    city: "Navi Mumbai",
    subjects: ["Python", "Bootstrap"],
    profile: { grade: "A", attendance: 93 }
  },
  {
    name: "Akshay",
    age: 20,
    city: "Saket",
    subjects: ["Python", "Math"],
    profile: { grade: "A", attendance: 96 }
  },
  {
    name: "Rajesh",
    age: 28,
    city: "Kolhapur",
    subjects: ["Python", "Go"],
    profile: { grade: "A", attendance: 95 }
  }
]);
```

**Verify Insertion:**

```javascript
db.students.find()
```

---

### **2. Read (Query Students)**

```javascript
// All students
db.students.find()

// Students from "Navi Mumbai"
db.students.find({ city: "Navi Mumbai" })

// Students with age > 21
db.students.find({ age: { $gt: 21 } })

// Students having "Python" as a subject
db.students.find({ subjects: { $in: ["Python"] } })

// Show only name and city (hide _id)
db.students.find({}, { name: 1, city: 1, _id: 0 })
```

---

### **3. Update (Modify Data)**

```javascript
// Update Akshay's city to "Delhi"
db.students.updateOne({ name: "Akshay" }, { $set: { city: "Delhi" } })

// Increase all students' age by 1
db.students.updateMany({}, { $inc: { age: 1 } })

// Add new subject "MongoDB" to Rajesh's subjects
db.students.updateOne({ name: "Rajesh" }, { $push: { subjects: "MongoDB" } })

// Replace Rajesh's profile entirely
db.students.updateOne(
  { name: "Rajesh" },
  { $set: { profile: { grade: "C", attendance: 45 } } }
)
```

**Check Updated Data:**

```javascript
db.students.find()
```

---

### **4. Delete (Remove Data)**

```javascript
// Delete student with city "Delhi"
db.students.deleteOne({ city: "Delhi" })

// Delete all students with age < 22
db.students.deleteMany({ age: { $lt: 22 } })
```

**Verify Deletions:**

```javascript
db.students.find()
```

---

### **5. Upsert Operation**

```javascript
db.students.updateOne(
  { name: "Ravi" },
  { $set: { name: "Ravi", age: 24, city: "Chennai" } },
  { upsert: true }
)
```

**Verify Upserted Document:**

```javascript
db.students.find()
```
---

# 📌 Task 3 – MongoDB Query Operators

This task covers **Comparison**, **Logical**, **Element**, **Array**, and **Evaluation** operators in MongoDB.
All queries are executed on the `students` collection inside the `learning_mongo` database.

---

## 1️⃣ Comparison Operators

**Find all students whose age is exactly 26**

```js
db.students.find({ age: { $eq: 26 } })
```

**Find students whose age is not equal to 26**

```js
db.students.find({ age: { $ne: 26 } })
```

**Find students whose age is greater than 24**

```js
db.students.find({ age: { $gt: 24 } })
```

**Find students whose age is less than 23**

```js
db.students.find({ age: { $lt: 23 } })
```

**Find students who live in either Pune or Satara**

```js
db.students.find({ city: { $in: ["Pune", "Satara"] } })
```

---

## 2️⃣ Logical Operators

**Find students whose age is greater than 24 AND city is Satara**

```js
db.students.find({
  $and: [{ age: { $gt: 24 } }, { city: "Satara" }]
})
```

**Find students whose city is Pune OR Navi Mumbai**

```js
db.students.find({
  $or: [{ city: "Pune" }, { city: "Navi Mumbai" }]
})
```

**Find students whose age is NOT greater than 25**

```js
db.students.find({ age: { $not: { $gt: 25 } } })
```

**Find students who are not from Pune and not younger than 22**

```js
db.students.find({
  $and: [
    { city: { $not: { $eq: "Pune" } } },
    { age: { $not: { $lt: 22 } } }
  ]
})
```

---

## 3️⃣ Element Operators

**Find students who have a profile field**

```js
db.students.find({ profile: { $exists: true } })
```

**Find students whose age field type is int**

```js
db.students.find({ age: { $type: "int" } })
```

---

## 4️⃣ Array Operators

**Find students whose subjects contain both Python and Math**

```js
db.students.find({ subjects: { $all: ["Python", "Math"] } })
```

**Find students who have exactly 2 subjects**

```js
db.students.find({ subjects: { $size: 2 } })
```

---

## 5️⃣ Evaluation Operators

**Find students whose name starts with "R"**

```js
db.students.find({ name: { $regex: "^R" } })
```

**Find students whose subjects contain the word Python (using \$text)**

```js
db.students.createIndex({ subjects: "text" })
db.students.find({ $text: { $search: "Python" } })
```

**Find students whose age is greater than 25 using \$expr**

```js
db.students.find({ $expr: { $gt: ["$age", 25] } })
```

---


