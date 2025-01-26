### 1. Create a Unique Index on Faculty Name
```javascript
db.Faculty.createIndex({ Name: 1 }, { unique: true });
```

### 2. Aggregate: Sum of Final Marks for All Courses
```javascript
db.Course.aggregate([
  {
    $group: {
      _id: null,
      TotalFinalMark: { $sum: "$FinalMark" }
    }
  }
]);
```

### 3. One-to-Many Relationship Between Student and Course
Add an array of Course IDs in the `student` object:
```javascript
db.student.updateMany({}, [
  {
    $set: {
      Courses: [101, 102] // Example Course IDs
    }
  }
]);
```

### 4. Select a Specific Student and Display Their Courses
```javascript
db.student.find(
  { FirstName: "Ali" },
  { FirstName: 1, LastName: 1, Courses: 1, _id: 0 }
);
```

### 5. One-to-One Relationship Between Student and Faculty Using DBRef
Add the Faculty object as a reference in the `student`:
```javascript
db.student.updateMany({}, [
  {
    $set: {
      Faculty: {
        $ref: "Faculty",
        $id: 1 // Example Faculty ID
      }
    }
  }
]);
```

### 6. Select a Specific Student and Display Their Faculty
```javascript
db.student.find(
  { FirstName: "Ali" },
  { FirstName: 1, LastName: 1, Faculty: 1, _id: 0 }
);
```

### 7. Count of All Students
```javascript
db.student.aggregate([
  {
    $group: {
      _id: null,
      StudentCount: { $sum: 1 }
    }
  }
]);
```

### 8. Students Count in Each Faculty
```javascript
db.student.aggregate([
  { $unwind: "$Faculty" },
  {
    $group: {
      _id: "$Faculty.Name",
      StudentCount: { $sum: 1 }
    }
  }
]);
```
