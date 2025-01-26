### 1. Create and Switch to Database
```javascript
use FacultySystemDB;
```

### 2. Create `student` Collection
Insert a document into the `student` collection with the following schema:
```javascript
db.student.insertOne({
  FirstName: "Ragheb",
  LastName: "Ahmed",
  Age: 20,
  Faculty: { Name: "Engineering", Address: "123 College St." },
  Grades: [
    { CourseName: "Mathematics", Grade: 85, Pass: true },
    { CourseName: "Physics", Grade: 78, Pass: true }
  ],
  IsFired: false
});
```

---

## Data Insertion

### Insert a Single Document
```javascript
db.student.insertOne({
  FirstName: "Ahmed",
  LastName: "Ali",
  Age: 22,
  Faculty: { Name: "Business", Address: "456 Finance Ave." },
  Grades: [
    { CourseName: "Accounting", Grade: 88, Pass: true },
    { CourseName: "Management", Grade: 72, Pass: true }
  ],
  IsFired: false
});

// Additional example:
db.student.insertOne({
  FirstName: "Sara",
  LastName: "Omar",
  Age: 19,
  Faculty: { Name: "Arts", Address: "789 Humanities Blvd." },
  Grades: [
    { CourseName: "History", Grade: 92, Pass: true },
    { CourseName: "Philosophy", Grade: 81, Pass: true }
  ],
  IsFired: true
});
```

### Insert Multiple Documents
```javascript
db.student.insertMany([
  {
    FirstName: "Ali",
    LastName: "Hassan",
    Age: 21,
    Faculty: { Name: "Medicine", Address: "101 Health Dr." },
    Grades: [
      { CourseName: "Biology", Grade: 80, Pass: true },
      { CourseName: "Anatomy", Grade: 77, Pass: true }
    ],
    IsFired: false
  },
  {
    FirstName: "Mariam",
    LastName: "Ahmed",
    Age: 23,
    Faculty: { Name: "Law", Address: "202 Justice Ln." },
    Grades: [
      { CourseName: "Criminal Law", Grade: 89, Pass: true },
      { CourseName: "Civil Law", Grade: 84, Pass: true }
    ],
    IsFired: false
  }
]);
```

---

## Data Retrieval

### Retrieve All Students
```javascript
db.student.find();
```

### Retrieve a Student by First Name
```javascript
db.student.find({ FirstName: "Ahmed" });
```

### Retrieve Students by Multiple Conditions
- First Name is "Ahmed" or Last Name is "Ahmed":
  ```javascript
  db.student.find({ $or: [{ FirstName: "Ahmed" }, { LastName: "Ahmed" }] });
  ```
- First Name is NOT "Ahmed":
  ```javascript
  db.student.find({ FirstName: { $ne: "Ahmed" } });
  ```
- Age is less than 21:
  ```javascript
  db.student.find({ Age: { $lt: 21 } });
  ```
- Students who are fired:
  ```javascript
  db.student.find({ IsFired: true });
  ```
- Age is 21 or older and Faculty is not null:
  ```javascript
  db.student.find({ $and: [{ Age: { $gte: 21 } }, { Faculty: { $ne: null } }] });
  ```

### Retrieve Specific Fields
```javascript
db.student.find(
  { FirstName: "Ahmed" },
  { FirstName: 1, LastName: 1, IsFired: 1, _id: 0 }
);
```

---

## Data Updates

### Update a Single Document
```javascript
db.student.updateOne(
  { FirstName: "Sara" },
  { $set: { LastName: "Mohamed" } }
);
```

### Update Multiple Documents
```javascript
db.student.updateMany(
  { IsFired: true },
  { $set: { IsFired: false } }
);
```

---

## Data Deletion

### Delete Specific Documents
- Delete fired students:
  ```javascript
  db.student.deleteMany({ IsFired: true });
  ```
- Delete all students:
  ```javascript
  db.student.deleteMany({});
  ```

### Drop the Database
```javascript
use FacultySystemDB;
db.dropDatabase();
```

---

## New Database and Collections

### Create and Switch to New Database
```javascript
use FacultySystemDBV2;
```

### Create `student` Collection
```javascript
db.student.insertMany([
  {
    FirstName: "Ali",
    LastName: "Hassan",
    IsFired: false,
    FacultyID: 1,
    Courses: [
      { CourseID: 101, Grade: 80 },
      { CourseID: 102, Grade: 85 }
    ]
  },
  {
    FirstName: "Mona",
    LastName: "Salim",
    IsFired: false,
    FacultyID: 2,
    Courses: [
      { CourseID: 103, Grade: 90 },
      { CourseID: 104, Grade: 87 }
    ]
  }
]);
```

### Create `Faculty` Collection
```javascript
db.Faculty.insertMany([
  { FacultyID: 1, Name: "Engineering", Address: "123 College St." },
  { FacultyID: 2, Name: "Arts", Address: "456 Arts Ave." }
]);
```

### Create `Course` Collection
```javascript
db.Course.insertMany([
  { CourseID: 101, Name: "Mathematics", FinalMark: 100 },
  { CourseID: 102, Name: "Physics", FinalMark: 100 },
  { CourseID: 103, Name: "History", FinalMark: 100 },
  { CourseID: 104, Name: "Philosophy", FinalMark: 100 }
]);
