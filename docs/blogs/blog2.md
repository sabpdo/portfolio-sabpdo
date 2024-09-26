---
title: "Blog 2: Reflection on Lecture 7 - Data Design"
layout: doc
---

# Blog 2: Reflection on Lecture 7 - Data Design

In Lecture 7, we explored various methods of designing databases, including the Object model, Relational model, and Document model. Each approach offers unique ways of structuring data, and I found it helpful to apply them to a real-world example like Canvas, a learning platform that many of us (including myself!) use daily, to better understand.

### Object Model

In the **Object model**, data is treated as objects. If Canvas were modeled using this approach, we could envision objects like `Course`, `Assignment`, `Student`, and `Teacher`.

![Object Model](/assets/images/Blogs/B2/object_model.png)

### Relational Model

In the **Relational model**, data is structured into tables with rows and columns, following a schema that defines relationships between tables. For Canvas, a relational database might include tables such as:

- **Assignments table**:
  ```
  id | course_id | grade | deadline | assignment_name
  ```
- **Courses table**:
  ```
  id | course_name | teacher_id | students
  ```
- **Students table**:
  ```
  id | student_name
  ```
- **Teacher table**:
  ```
  id | teacher_name
  ```


### Document Model

The **Document model** stores data in a more flexible, schema-less format, often using JSON-like structures. In MongoDB, for example, Canvas data might be stored as documents that embed related data within a single document. Here’s how a document for an assignment might look (structured as a json):

```json
{
  "_id": "assignment1",
  "course": {
    "course_id": "course1",
    "name": "Software Design",
    "teacher": "Max Goldman & Arvind Satyanarayan",
    "students": {
        "student_id": "student1",
        "name": "Sabrina Do"
    },
  },
  "assignment_name": "Homework 1",
  "grade": 90,
  "deadline": "2024-09-26"
}
```
While this is just one representation, it could instead be structured such that the course is the outermost structure/document. The flexibility in choosing the structure allows for easy querying in this document-based structure. However, I would argue that database design becomes much more intentional with the document model as one has to determine which values are nested and which are not.

### Concept-Based Approach
For Canvas, we can break it down like this:

1. **Concept**: Courses  
   **Purpose**: 
   Organize content, assignments, and students into a single class. 
   **State**: 

   name: Course -> __one__ Name/String

   teacher: Course -> __set__ Teacher

   student: Course -> __set__ Student

   assignments: Course -> __set__ Assignment

2. **Concept**: Assignments  
   **Purpose**: 
   Track student progress and grades on specific tasks 
   **State**: 

   name: Assignment -> __one__ Name/String

   deadline: Assignment -> __one__ Date

   grade: Assignment -> __set__ Grades

Once these concepts are identified, we can translate them into a MongoDB schema that reflects their purpose and state.

```
interface Course {
  _id: ObjectId,
  name: String,
  teacher: [ObjectId], 
  students: [ObjectId], 
  assignments: [ObjectId] 
}

interface Assignment {
  _id: ObjectId,
  name: String,
  deadline: Date,
  grades: [ObjectId] 
}
```

Combined concept:
```
interface Course {
  _id: ObjectId,
  name: String,
  teacher: ObjectId,
  students: [
    { studentId: ObjectId, name: String }, 
  ],
  assignments: [
    { 
      assignmentId: ObjectId, 
      name: String, 
      deadline: Date, 
      grades: [ { studentId: ObjectId, grade: Number } ] 
    }
  ]
}
```

Overall, exploring the Object, Relational, and Document models through the lens of Canvas has provided valuable insights into how different database design approaches shape the way we store and interact with data. There are numerous trade-offs involved in database design and thoughtful choices can optimize both performance and usability.