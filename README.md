# MDB100: MongoDB Database and Security

 A complete beginner-to-intermediate course covering MongoDB storage, retrieval, CRUD operations, and enterprise-grade security concepts, with hands-on demos using mongosh.

## Module 1: MongoDB Overview & Architecture
What is MongoDB?
- NoSQL, document-oriented database
- Stores data as BSON (Binary JSON)
- Schema-flexible

### Core Concepts
* Database → Collection → Document
* Replica Sets (high availability)
* Sharding (horizontal scaling)

### Demo: Start MongoDB
```
mongod --dbpath /data/db
mongosh
```

## Module 2: Storage and Retrieval
### How MongoDB Stores Data
* Documents stored in collections
* Indexes stored separately for fast lookup

### Retrieval Basics
```
use school
db.students.find()
```
## Module 3: Creating Documents
### Single Insert
```
db.students.insertOne({
  name: "Asha",
  age: 21,
  courses: ["Math", "CS"]
})
```
### Bulk Inserts
```
db.students.insertMany([
  { name: "Ravi", age: 22 },
  { name: "Neha", age: 20 }
])
```
### Bulk vs Single Writes

| Single Write   | Bulk Write |
| ------------- | ------------- |
| Atomic  | Faster for large data   |
| Simple  | Optimized network usage  |

## Module 4: Querying Data
**Basic Query Operators (*)**
* When you only care about which documents match
- It answers:
  “Which documents do I want?”
* ✅ When you need to filter data based on values
```
db.students.find({ age: { $gte: 18 } })
```

**Filtering and Projection (*)**

* This combines two different actions in a query:

| Part | Purpose |
| --- | --- |
| Filtering | Choose which documents |
| Projection | Choose which fields |

- It answers:
   “Which documents AND which fields from them?”
  
* When you want to reduce data transfer and improve performance

```
db.students.find(
  { age: { $gte: 18 } },         // Filtering
  { name: 1, age: 1, _id: 0 }   // Projection
)
```
**Using Cursors (*)**
- What it does
- A cursor is a pointer to the result set returned by find().
- MongoDB does not return all documents at once—it returns them in batches.

- It answers: “How do I process large result sets efficiently?”
- ✅ When handling large datasets or streaming results
```
const cursor = db.students.find({ age: { $gte: 18 } })

cursor.forEach(doc => {
  print(doc.name)
})
```

## Module 5: Advanced Query Operators
### Range Operators (*)
```
db.students.find({ age: { $gt: 18, $lt: 25 } })
```
### Logical Operators (*)
```
  db.students.find({
  $and: [ { age: { $gt: 20 } }, { name: "Asha" } ]
})
```
### Array Operators (*)
```
db.students.find({ courses: { $in: ["CS"] } })
```
## Module 6: Update Operations
### Basic Update Operations (*)
```
db.students.updateOne(
  { name: "Asha" },
  { $set: { age: 22 } }
)
```
### Relative Update Operations (*)
```
db.students.updateOne(
  { name: "Asha" },
  { $inc: { age: 1 } }
)
```
- Updating, Locking, and Concurrency
- Document-level locking
- Atomic operations per document
- Optimistic concurrency control

## Module 7: Deleting Documents
```
db.students.deleteOne({ name: "Ravi" })
```
```
db.students.deleteMany({ age: { $lt: 18 } })
```

## Module 8: MongoDB Security Fundamentals
- Security Layers
- Authentication
- Authorization
- Encryption
- Auditing

## Module 9: Authentication Models
- SCRAM Authentication (Default)
- Username/password based
- X.509 Certificates
- Certificate-based auth
- LDAP Authentication
   - Centralized enterprise authentication

**Demo: Create User**
```
use admin
db.createUser({
  user: "dbAdmin",
  pwd: "StrongPass123",
  roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
})
```
### Module 10: Authorization & Roles
- Role-Based Access Control (RBAC)
- Built-in Roles:
  - read
  - readWrite
  - dbAdmin
  - clusterAdmin

Demo: Assign Role
db.grantRolesToUser(
  "dbAdmin",
  [ { role: "readWrite", db: "school" } ]
)
Module 11: LDAP Integration
LDAP Use Cases

Corporate Active Directory

Central user management

Configuration (Conceptual)
security:
  authorization: enabled
  ldap:
    servers: ldap.example.com
Module 12: Encryption
Encryption In Flight

TLS/SSL

Protects data between client and server

Encryption At Rest

Encrypted storage engine

Protects disk data

Encryption In Use

Client-side field-level encryption

Module 13: Auditing
What is Auditing?

Tracks database activity

Required for compliance

Audit Events

Authentication attempts

CRUD operations

Role changes

Module 14: Additional Security Measures

IP Whitelisting

Network isolation

Regular backups

Index access control

Monitoring and alerts

Final Hands-On Demo: Secure Database Setup

Enable authentication

Create admin user

Assign least-privilege roles

Enable TLS

Enable auditing

Course Completion Outcomes

By the end of this course, you will be able to:

Design and query MongoDB databases

Perform CRUD operations efficiently

Manage concurrency and updates

Secure MongoDB using industry best practices

Recommended Practice

MongoDB Atlas Free Tier

MongoDB Compass

MongoDB University (M001, M103)

End of MDB100 Course
