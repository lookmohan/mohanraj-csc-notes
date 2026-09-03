Here are your complete, beginner-friendly MongoDB teaching notes. Designed for classroom teaching, they follow your specified structure for every topic and use a consistent `college` database with `students`, `courses`, and `teachers` collections.

---

### MongoDB Teaching Notes: From Zero to Hero

**Welcome, students!** These notes are designed for complete beginners. We will learn MongoDB step-by-step, using simple English and practical examples.

---

### MODULE 1 – INTRODUCTION TO DATABASES AND MONGODB

#### 1. What is a Database?
- **What is it?** A place to store and organize data.
- **Simple Explanation:** Think of a database as a digital filing cabinet. Instead of paper files, it stores information on a computer.
- **Why do we use it?** To store, find, and manage information (data) easily.
- **Real-world example:** Your phone's contact list. It stores names, phone numbers, and emails, and you can search for a person instantly.

#### 2. What is MongoDB?
- **What is it?** MongoDB is a popular **NoSQL** database. It stores data in flexible, JSON-like documents.
- **Simple Explanation:** Imagine a library where instead of organized bookshelves (like in SQL), every book (document) can have different chapters and formats. MongoDB is like that library for data.
- **Why do we use it?** Because it's flexible, fast, and great for handling lots of data that doesn't fit nicely into tables.
- **Real-world example:** An e-commerce website storing product details. Each product might have different attributes (e.g., a phone has a 'camera' field, a book has an 'author' field). MongoDB handles this easily.

#### 3. What is NoSQL?
- **What is it?** A type of database that is not based on tables and rows like traditional SQL databases.
- **Simple Explanation:** If SQL databases are like strict spreadsheets (rows and columns), NoSQL databases are like flexible folders (documents) where you can store various information.
- **Why do we use it?** For flexibility, scalability, and handling large volumes of data.

#### 4. SQL vs NoSQL
| Feature | SQL (e.g., MySQL, PostgreSQL) | NoSQL (e.g., MongoDB) |
| :--- | :--- | :--- |
| **Structure** | Tables, Rows, Columns | Collections, Documents, Fields |
| **Schema** | Fixed (schema is defined before inserting data). | Dynamic (data can have different fields). |
| **Flexibility** | Less flexible for changing data structure. | Very flexible. You can add new fields anytime. |
| **Use Case** | Banking systems, ERP, where data integrity is critical. | Content management, real-time analytics, big data. |

#### 5. Advantages of MongoDB
- **Flexibility:** You can change the data structure easily.
- **Speed:** Fast to query and scale.
- **Scalability:** Great for handling huge amounts of data and traffic.
- **Document-Oriented:** Uses JSON-like documents, which are similar to objects in programming.

#### 6. Real-world Applications
- E-commerce platforms (like Shopify).
- Social media sites (like Twitter).
- Content management systems.
- Gaming applications (storing player data).

#### 7. Core Concepts (The "MongoDB Alphabet")
- **Database:** The container for all your data. Think of a filing cabinet.
    - **Example:** `college`
- **Collection:** A group of documents. Like a folder inside the cabinet.
    - **Example:** `students`, `courses`
- **Document:** A single piece of information. Like a single file inside the folder.
    - **Example:** `{ name: "Arun", age: 20 }`
- **Field:** A key-value pair in a document. Like a piece of data on a file.
    - **Example:** `name: "Arun"`
- **BSON:** The format MongoDB uses to store data. It is like JSON but with more data types.
- **_id:** A unique identifier for every document. MongoDB automatically creates it.

#### 8. MongoDB Data Types
These are the most common types:
- **String:** For text. `{ name: "Arun" }`
- **Integer:** For whole numbers. `{ age: 20 }`
- **Boolean:** For true/false. `{ isGraduated: false }`
- **Array:** For lists. `{ skills: ["Python", "SQL"] }`
- **Object:** For embedded documents (nested data). `{ address: { city: "Chennai", pincode: 600001 } }`

---

### MODULE 2 – SETUP AND CONNECTION

#### 1. MongoDB Installation (Local)
1.  Go to the MongoDB website and download the Community Server.
2.  Run the installer.
3.  During installation, also install **MongoDB Compass** (the GUI).

#### 2. MongoDB Compass
- **What is it?** A graphical user interface (GUI) for MongoDB. You can see your data visually.
- **Why do we use it?** To easily browse, add, and edit data without typing commands.

#### 3. mongosh (MongoDB Shell)
- **What is it?** A command-line interface to interact with your MongoDB server.
- **Why do we use it?** It's powerful for administration, scripting, and learning the commands. We will use `mongosh` for most of our examples.

#### 4. MongoDB Atlas (Cloud)
- **What is it?** MongoDB's cloud database service.
- **Why do we use it?** You don't have to install anything on your computer. It’s free to start and accessible from anywhere.

#### 5. Connecting to MongoDB
- In `mongosh`, if you have it installed locally, you simply type `mongosh` in your terminal/command prompt.
- To connect via Python, you use a connection string (we will see this later).

#### 6. Basic Shell Commands
- **Show all databases:** `show dbs`
- **Use (or create) a database:** `use college`
- **Show current database:** `db`

---

### MODULE 3 – DATABASE AND COLLECTIONS

#### 1. Creating a Database
- **What is it?** Creating a new container for your data.
- **Syntax:**
    ```mongosh
    use <database_name>
    ```
- **Simple Example:**
    ```mongosh
    use college
    ```
- **Expected Output:** `switched to db college`
- **Explanation:** In MongoDB, a database is not actually created until you insert data into it.

#### 2. Showing Databases
- **Syntax:**
    ```mongosh
    show dbs
    ```
- **Explanation:** Lists all databases that contain at least one collection with data.

#### 3. Creating a Collection Explicitly
- **What is it?** A collection is created automatically when you insert a document. You can also create it manually.
- **Why do we use it?** To create a collection with specific options (e.g., capped collections, which are fixed-size).
- **Syntax:**
    ```mongosh
    db.createCollection("teachers")
    ```
- **Explanation:** Creates a new collection named `teachers`.

#### 4. Showing Collections
- **Syntax:**
    ```mongosh
    show collections
    ```
- **Explanation:** Lists all collections in the current database.

#### 5. Dropping a Collection
- **What is it?** Permanently deletes a collection and all its documents.
- **Syntax:**
    ```mongosh
    db.students.drop()
    ```
- **Explanation:** This will delete the `students` collection. Be very careful!

#### 6. Dropping a Database
- **What is it?** Permanently deletes the entire database you are using.
- **Syntax:**
    ```mongosh
    db.dropDatabase()
    ```
- **Explanation:** This will delete the `college` database. Be very careful!

---

### MODULE 4 – CRUD OPERATIONS (Create, Read, Update, Delete)

This is the core of any database. All our examples will use the `college` database and the `students` collection.

- **Student Document Structure:** `{ name: "Arun", age: 20, course: "Python", city: "Chennai", marks: 85, skills: ["Python", "SQL"] }`

#### 1. insertOne()
- **What is it?** Adds one new document to a collection.
- **Syntax:**
    ```mongosh
    db.collection_name.insertOne({ ... })
    ```
- **Simple Example:**
    ```mongosh
    db.students.insertOne({
        name: "Priya",
        age: 22,
        course: "Java",
        city: "Mumbai",
        marks: 92,
        skills: ["Java", "C++"]
    })
    ```
- **Expected Output:**
    ```json
    {
      "acknowledged" : true,
      "insertedId" : ObjectId("...")
    }
    ```
- **Line-by-Line Explanation:**
    1.  `db.students` : Select the `students` collection in the current database (`college`).
    2.  `.insertOne({ ... })` : The command to insert a single document.
    3.  The JSON object inside `{ }` is the data we are inserting.
- **Real-world Example:** A student enrolling in a new course.
- **Common Mistakes:** Forgetting commas between fields.

#### 2. insertMany()
- **What is it?** Adds multiple documents to a collection in one go.
- **Syntax:**
    ```mongosh
    db.collection_name.insertMany([ {...}, {...} ])
    ```
- **Simple Example:**
    ```mongosh
    db.students.insertMany([
        { name: "Ravi", age: 21, course: "Python", city: "Delhi", marks: 78, skills: ["Python", "JavaScript"] },
        { name: "Sneha", age: 19, course: "Web Dev", city: "Chennai", marks: 95, skills: ["React", "NodeJS"] }
    ])
    ```
- **Explanation:** The documents must be inside an array `[ ]`, separated by commas.

#### 3. find()
- **What is it?** Retrieves (reads) documents from a collection.
- **Syntax:** `db.collection_name.find({query})`
- **Simple Example (Find all students):**
    ```mongosh
    db.students.find({})
    ```
- **Expected Output:** All the documents in the `students` collection.
- **Explanation:** `find({})` with an empty query `{}` returns all documents.
- **Common Mistakes:** Forgetting the `{}` in `find()`.

#### 4. findOne()
- **What is it?** Retrieves only the first document that matches the query.
- **Syntax:**
    ```mongosh
    db.collection_name.findOne({query})
    ```
- **Simple Example:**
    ```mongosh
    db.students.findOne({ name: "Arun" })
    ```
- **Expected Output:** The first document where the `name` is "Arun".
- **Explanation:** Useful when you only need one result.

#### 5. updateOne()
- **What is it?** Updates only the first document that matches the filter.
- **Syntax:**
    ```mongosh
    db.collection_name.updateOne( {filter}, { $set: {field: new_value} } )
    ```
- **Simple Example:**
    ```mongosh
    db.students.updateOne(
        { name: "Arun" },
        { $set: { city: "Hyderabad" } }
    )
    ```
- **Expected Output:**
    ```json
    { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
    ```
- **Explanation:**
    - `{ name: "Arun" }` is the filter to find the student.
    - `{ $set: { city: "Hyderabad" } }` uses the `$set` operator to change the city value.

#### 6. updateMany()
- **What is it?** Updates all documents that match the filter.
- **Syntax:**
    ```mongosh
    db.collection_name.updateMany( {filter}, { $set: {field: new_value} } )
    ```
- **Simple Example:**
    ```mongosh
    db.students.updateMany(
        { course: "Python" },
        { $set: { city: "Bangalore" } }
    )
    ```
- **Explanation:** This will update the city to "Bangalore" for all students taking the "Python" course.

#### 7. deleteOne()
- **What is it?** Deletes only the first document that matches the filter.
- **Syntax:**
    ```mongosh
    db.collection_name.deleteOne( {filter} )
    ```
- **Simple Example:**
    ```mongosh
    db.students.deleteOne( { name: "Ravi" } )
    ```
- **Expected Output:**
    ```json
    { "acknowledged" : true, "deletedCount" : 1 }
    ```

#### 8. deleteMany()
- **What is it?** Deletes all documents that match the filter.
- **Syntax:**
    ```mongosh
    db.collection_name.deleteMany( {filter} )
    ```
- **Simple Example:**
    ```mongosh
    db.students.deleteMany( { city: "Delhi" } )
    ```
- **Explanation:** This will delete all students whose city is "Delhi".

---

### MODULE 5 – QUERY OPERATORS

These are used with `find()` to build powerful queries. Let's insert some sample data first.

```mongosh
db.students.insertMany([
    { name: "Arun", age: 20, course: "Python", city: "Chennai", marks: 85, skills: ["Python", "SQL"] },
    { name: "Priya", age: 22, course: "Java", city: "Mumbai", marks: 92, skills: ["Java", "C++"] },
    { name: "Ravi", age: 21, course: "Python", city: "Delhi", marks: 78, skills: ["Python", "JavaScript"] },
    { name: "Sneha", age: 19, course: "Web Dev", city: "Chennai", marks: 95, skills: ["React", "NodeJS"] }
])
```

- **`$gt` (Greater Than):**
    - **Syntax:** `{ field: { $gt: value } }`
    - **Example:** `db.students.find( { marks: { $gt: 80 } } )`
    - **Output:** `Priya` and `Sneha` (marks 92 and 95).
- **`$gte` (Greater Than or Equal To):**
    - **Example:** `db.students.find( { marks: { $gte: 85 } } )`
    - **Output:** `Arun`, `Priya`, and `Sneha`.
- **`$lt` (Less Than):**
    - **Example:** `db.students.find( { age: { $lt: 21 } } )`
    - **Output:** `Sneha` (age 19).
- **`$lte` (Less Than or Equal To):**
    - **Example:** `db.students.find( { age: { $lte: 21 } } )`
    - **Output:** `Arun`, `Ravi`, and `Sneha`.
- **`$eq` (Equal To):**
    - **Example:** `db.students.find( { city: { $eq: "Chennai" } } )`
    - **Output:** `Arun` and `Sneha`.
- **`$ne` (Not Equal To):**
    - **Example:** `db.students.find( { course: { $ne: "Python" } } )`
    - **Output:** `Priya` and `Sneha`.
- **`$in` (In Array):**
    - **Example:** `db.students.find( { city: { $in: ["Chennai", "Delhi"] } } )`
    - **Output:** `Arun`, `Ravi`, and `Sneha`.
- **`$nin` (Not In Array):**
    - **Example:** `db.students.find( { course: { $nin: ["Python", "Java"] } } )`
    - **Output:** `Sneha` (Web Dev).

**Exercise:**
- **Question:** Find all students who are 20 years old or older but less than 22?
- **Answer:** `db.students.find( { age: { $gte: 20, $lt: 22 } } )` (Arun and Ravi)

---

### MODULE 6 – LOGICAL OPERATORS

#### 1. `$and`
- **What is it?** Matches documents that satisfy **all** conditions.
- **Syntax:** `{ $and: [ {cond1}, {cond2}, ... ] }`
- **Simple Example:** Find students from Chennai who are over 20.
    ```mongosh
    db.students.find( { $and: [ { city: "Chennai" }, { age: { $gt: 20 } } ] } )
    ```
    (Output: Sneha is 19, so only Arun and Sneha? Wait. Arun is 20, so he is not greater than 20. Let's use `{ $and: [ { city: "Chennai" }, { age: { $gte: 20 } } ] }` which gives `Arun` and `Sneha`.)

#### 2. `$or`
- **What is it?** Matches documents that satisfy **at least one** condition.
- **Syntax:** `{ $or: [ {cond1}, {cond2}, ... ] }`
- **Simple Example:** Find students from Chennai OR who are over 21.
    ```mongosh
    db.students.find( { $or: [ { city: "Chennai" }, { age: { $gt: 21 } } ] } )
    ```
    (Output: Arun, Priya (22), Sneha)

#### 3. `$not`
- **What is it?** Matches documents that **do not** satisfy a condition.
- **Syntax:** `{ field: { $not: { operator } } }`
- **Simple Example:** Find students who are NOT from Chennai.
    ```mongosh
    db.students.find( { city: { $not: { $eq: "Chennai" } } } )
    ```
    (Output: Priya, Ravi)

#### 4. `$nor`
- **What is it?** Matches documents that fail **all** conditions.
- **Syntax:** `{ $nor: [ {cond1}, {cond2}, ... ] }`
- **Simple Example:** Find students who are not from Chennai and not learning Java.
    ```mongosh
    db.students.find( { $nor: [ { city: "Chennai" }, { course: "Java" } ] } )
    ```
    (Output: Ravi)

---

### MODULE 7 – PROJECTION AND RESULT HANDLING

#### 1. Projection
- **What is it?** Selecting specific fields to show in the result, like choosing only certain columns in SQL.
- **Why do we use it?** To limit network bandwidth and get only the data you need.

#### 2. Including Fields
- **Syntax:** `db.collection.find({query}, { field1: 1, field2: 1 })`
- **Simple Example:** Show only `name` and `marks` for all students.
    ```mongosh
    db.students.find({}, { name: 1, marks: 1 })
    ```

#### 3. Excluding Fields
- **Syntax:** `db.collection.find({query}, { field1: 0, field2: 0 })`
- **Simple Example:** Show all fields except `age` and `city`.
    ```mongosh
    db.students.find({}, { age: 0, city: 0 })
    ```

#### 4. `_id: 0`
- **Why do we use it?** By default, `_id` is always shown. To hide it, you must explicitly exclude it.
- **Simple Example:**
    ```mongosh
    db.students.find({}, { name: 1, marks: 1, _id: 0 })
    ```

#### 5. `sort()`
- **What is it?** Orders the results. Use `1` for ascending, `-1` for descending.
- **Syntax:** `.sort({ field: 1 or -1 })`
- **Simple Example:** Sort students by marks descending.
    ```mongosh
    db.students.find({}).sort({ marks: -1 })
    ```

#### 6. `limit()`
- **What is it?** Limits the number of documents returned.
- **Syntax:** `.limit(number)`
- **Simple Example:** Get only the top 2 students by marks.
    ```mongosh
    db.students.find({}).sort({ marks: -1 }).limit(2)
    ```

#### 7. `skip()`
- **What is it?** Skips a number of documents.
- **Syntax:** `.skip(number)`
- **Simple Example:** Skip the first 2 documents and show the rest.
    ```mongosh
    db.students.find({}).skip(2)
    ```

#### 8. `countDocuments()`
- **What is it?** Counts the number of documents matching a query.
- **Syntax:** `.countDocuments({query})`
- **Simple Example:** Count how many students are from Chennai.
    ```mongosh
    db.students.countDocuments({ city: "Chennai" })
    ```
    **Output:** `2`

---

### MODULE 8 – UPDATE OPERATORS

#### 1. `$set`
- **What is it?** Sets the value of a field. If the field doesn't exist, it creates it.
- **Syntax:** `{ $set: { field: value } }`
- **Example:** Set `city` to "Pune" for the student named "Ravi".
    ```mongosh
    db.students.updateOne({ name: "Ravi" }, { $set: { city: "Pune" } })
    ```

#### 2. `$unset`
- **What is it?** Removes a field from the document.
- **Syntax:** `{ $unset: { field: "" } }`
- **Example:** Remove the `city` field from Priya's document.
    ```mongosh
    db.students.updateOne({ name: "Priya" }, { $unset: { city: "" } })
    ```

#### 3. `$inc` (Increment)
- **What is it?** Increases or decreases the value of a numeric field.
- **Syntax:** `{ $inc: { field: value } }`
- **Example:** Add 5 marks to Arun.
    ```mongosh
    db.students.updateOne({ name: "Arun" }, { $inc: { marks: 5 } })
    ```

#### 4. `$rename`
- **What is it?** Renames a field name.
- **Syntax:** `{ $rename: { old_name: "new_name" } }`
- **Example:** Rename `city` to `location`.
    ```mongosh
    db.students.updateMany({}, { $rename: { city: "location" } })
    ```

#### 5. Upsert
- **What is it?** A combination of "Update" and "Insert".
- **Why do we use it?** If a document matches the filter, it's updated. If not, a new document is inserted.
- **Syntax:** `{ upsert: true }`
- **Example:** Try to find a student named "Kiran" and update their marks. If they don't exist, create them.
    ```mongosh
    db.students.updateOne(
        { name: "Kiran" },
        { $set: { name: "Kiran", marks: 88, course: "MongoDB" } },
        { upsert: true }
    )
    ```

---

### MODULE 9 – ARRAYS

#### 1. Arrays in MongoDB
- **What is it?** A field that holds a list of values. `skills: ["Python", "SQL"]`.

#### 2. Searching Arrays
- To find a document where an array contains a specific value, just use `{ field: value }`.
- **Example:** Find all students who know Python.
    ```mongosh
    db.students.find({ skills: "Python" })
    ```
    (Output: Arun and Ravi)

#### 3. `$push`
- **What is it?** Adds an element to an array.
- **Syntax:** `{ $push: { field: value } }`
- **Example:** Add "HTML" to Arun's skills.
    ```mongosh
    db.students.updateOne({ name: "Arun" }, { $push: { skills: "HTML" } })
    ```

#### 4. `$pop`
- **What is it?** Removes the first or last element of an array.
- **Syntax:** `{ $pop: { field: 1 } }` (removes last), `{ $pop: { field: -1 } }` (removes first).
- **Example:** Remove the last skill from Priya's array.
    ```mongosh
    db.students.updateOne({ name: "Priya" }, { $pop: { skills: 1 } })
    ```

#### 5. `$pull`
- **What is it?** Removes all occurrences of a specific value from the array.
- **Syntax:** `{ $pull: { field: value } }`
- **Example:** Remove "SQL" from Arun's skills.
    ```mongosh
    db.students.updateOne({ name: "Arun" }, { $pull: { skills: "SQL" } })
    ```

#### 6. `$addToSet`
- **What is it?** Adds a value to an array only if it doesn't already exist (prevents duplicates).
- **Syntax:** `{ $addToSet: { field: value } }`
- **Example:** Add "Python" to Sneha's skills (only if she doesn't have it).
    ```mongosh
    db.students.updateOne({ name: "Sneha" }, { $addToSet: { skills: "Python" } })
    ```

---

### MODULE 10 – EMBEDDED DOCUMENTS

#### 1. Nested Documents
- **What is it?** Documents inside documents. It's a way to structure related data together.
- **Why do we use it?** For organization and to avoid joining data from different collections.

#### 2. Dot Notation
- **What is it?** A way to access fields inside embedded documents using a dot `.`.
- **Syntax:** `"outerField.innerField"`
- **Example:** Let's embed the address in the student document.

    ```mongosh
    db.students.insertOne({
        name: "Vikram",
        age: 23,
        address: {
            city: "Bangalore",
            state: "Karnataka",
            pincode: 560001
        },
        course: "Data Science"
    })
    ```

#### 3. Searching Nested Fields
- **Example:** Find all students whose city is "Bangalore".
    ```mongosh
    db.students.find({ "address.city": "Bangalore" })
    ```
    **Important:** Always put the dot-notated field in quotes `""`.

#### 4. Updating Nested Fields
- **Example:** Update Vikram's pincode.
    ```mongosh
    db.students.updateOne(
        { name: "Vikram" },
        { $set: { "address.pincode": 560002 } }
    )
    ```

---

### MODULE 11 – AGGREGATION PIPELINE

#### 1. What is Aggregation?
- **What is it?** A way to process multiple documents and return computed results. It's like SQL's `GROUP BY` with more power.
- **Simple Explanation:** Imagine taking all the student records and running them through a series of pipes. Each pipe performs an operation (like filtering, grouping, sorting).

#### 2. Aggregation Pipeline
- **Syntax:** `db.collection.aggregate([ {stage1}, {stage2}, ... ])`

#### 3. `$match`
- **What is it?** Filters the documents. Similar to `find()`.
- **Example:** Filter only students with marks > 80.
    ```mongosh
    db.students.aggregate([ { $match: { marks: { $gt: 80 } } } ])
    ```

#### 4. `$group`
- **What is it?** Groups documents by a field.
- **Example:** Group students by their course and find the average marks.
    ```mongosh
    db.students.aggregate([
        { $group: { _id: "$course", averageMarks: { $avg: "$marks" } } }
    ])
    ```
    `_id: "$course"` means group by the `course` field. The `$` is used to refer to the field name.

#### 5. `$sum`
- **What is it?** Calculates the total.
- **Example:** Count the number of students in each course.
    ```mongosh
    db.students.aggregate([
        { $group: { _id: "$course", studentCount: { $sum: 1 } } }
    ])
    ```

#### 6. `$avg`
- **What is it?** Calculates the average.
- **Example:** Shown above.

#### 7. `$min` & `$max`
- **What are they?** Find the minimum and maximum values.
- **Example:** Find the minimum and maximum marks in the database.
    ```mongosh
    db.students.aggregate([
        { $group: { _id: null, minMarks: { $min: "$marks" }, maxMarks: { $max: "$marks" } } }
    ])
    ```

#### 8. `$count`
- **What is it?** Counts the number of documents.
- **Example:** Count total students.
    ```mongosh
    db.students.aggregate([ { $count: "totalStudents" } ])
    ```

#### 9. `$sort`
- **What is it?** Sorts the documents in the pipeline.
- **Example:** After grouping, sort the courses by average marks descending.
    ```mongosh
    db.students.aggregate([
        { $group: { _id: "$course", avgMarks: { $avg: "$marks" } } },
        { $sort: { avgMarks: -1 } }
    ])
    ```

#### 10. `$project`
- **What is it?** Selects which fields to show in the result. Like projection in `find()`.
- **Example:** Show only the course name and average marks.
    ```mongosh
    db.students.aggregate([
        { $group: { _id: "$course", avgMarks: { $avg: "$marks" } } },
        { $project: { course: "$_id", avgMarks: 1, _id: 0 } }
    ])
    ```

#### 11. `$limit`
- **What is it?** Limits the number of documents output.
- **Example:** Get the top 2 courses by average marks.
    ```mongosh
    db.students.aggregate([
        { $group: { _id: "$course", avgMarks: { $avg: "$marks" } } },
        { $sort: { avgMarks: -1 } },
        { $limit: 2 }
    ])
    ```

---

### MODULE 12 – INDEXING

#### 1. What is an Index?
- **What is it?** A special data structure that stores a small portion of the data in an easy-to-search form.
- **Simple Explanation:** Think of the index at the back of a book. Instead of reading the whole book to find a topic, you go to the index, see the page number, and go directly there.

#### 2. Why Indexes are Used
- **Speed!** They make `find()` queries extremely fast, especially on large collections.
- **Performance:** Without indexes, MongoDB must scan every document, which is slow.

#### 3. createIndex()
- **Syntax:** `db.collection.createIndex( { field: 1 } )`
- **Example:** Create an ascending index on the `name` field.
    ```mongosh
    db.students.createIndex({ name: 1 })
    ```
    (For text search, use `"text"` as the index type.)

#### 4. getIndexes()
- **What is it?** Shows all indexes on a collection.
- **Syntax:** `db.collection.getIndexes()`
- **Example:**
    ```mongosh
    db.students.getIndexes()
    ```

#### 5. dropIndex()
- **What is it?** Deletes an index.
- **Syntax:** `db.collection.dropIndex({ field: 1 })`
- **Example:**
    ```mongosh
    db.students.dropIndex({ name: 1 })
    ```

---

### MODULE 13 – TOOLS

#### 1. MongoDB Compass
- **GUI:** Helps you visualize your data.
- **Visual Query Builder:** You can build queries by clicking instead of typing.
- **Explain Plan:** Shows you how a query is executed and if indexes are used.

#### 2. MongoDB Atlas
- **Cloud:** No installation required.
- **Free Tier:** Good for learning and small projects.
- **Features:** Backups, monitoring, and easy scaling.

#### 3. mongosh
- **The Shell:** We've been using it all along.
- **Scripting:** You can write JavaScript scripts to automate tasks.

#### 4. Import/Export Basics
- **`mongoimport`:** Import data from a JSON or CSV file.
    - `mongoimport --db college --collection students --file students.json`
- **`mongoexport`:** Export data to a JSON or CSV file.
    - `mongoexport --db college --collection students --out students.json`

---

### MODULE 14 – PYTHON + MONGODB (PyMongo)

#### 1. What is PyMongo?
- **What is it?** A Python library that allows your Python code to talk to MongoDB.
- **Why do we use it?** To use MongoDB inside your Python applications (e.g., a website or a data analysis script).

#### 2. Installing PyMongo
- **Command:** `pip install pymongo`
- **Explanation:** This downloads and installs the library so you can use it in your Python scripts.

#### 3. MongoDB Connection
- **Example:**
    ```python
    from pymongo import MongoClient

    # Replace the connection string with your own
    client = MongoClient('mongodb://localhost:27017/')

    # Select the database
    db = client['college']

    # Select the collection
    students_collection = db['students']
    print("Connected successfully!")
    ```

#### 4. Insert (Python)
- **Example:**
    ```python
    student_data = {
        "name": "Alex",
        "age": 24,
        "course": "MongoDB",
        "city": "New York",
        "marks": 88
    }
    result = students_collection.insert_one(student_data)
    print(f"Inserted document with _id: {result.inserted_id}")
    ```

#### 5. Read (Python)
- **Example (Find all):**
    ```python
    for student in students_collection.find({}):
        print(student)
    ```
- **Example (Find one):**
    ```python
    student = students_collection.find_one({"name": "Arun"})
    print(student)
    ```

#### 6. Update (Python)
- **Example:**
    ```python
    result = students_collection.update_one(
        {"name": "Alex"},
        {"$set": {"city": "Boston"}}
    )
    print(f"Modified {result.modified_count} document")
    ```

#### 7. Delete (Python)
- **Example:**
    ```python
    result = students_collection.delete_one({"name": "Alex"})
    print(f"Deleted {result.deleted_count} document")
    ```

#### 8. Complete Python CRUD Example
```python
from pymongo import MongoClient

# --- Connect ---
client = MongoClient('mongodb://localhost:27017/')
db = client['college']
students = db['students']

# --- CREATE (Insert) ---
students.insert_one({"name": "Lena", "course": "AI", "marks": 90})

# --- READ (Find One) ---
print(students.find_one({"name": "Lena"}))

# --- UPDATE ---
students.update_one({"name": "Lena"}, {"$set": {"marks": 95}})

# --- READ (After Update) ---
print(students.find_one({"name": "Lena"}))

# --- DELETE ---
students.delete_one({"name": "Lena"})

# --- CLOSE ---
client.close()
```

---

### MODULE 15 – PRACTICE EXERCISES

#### A. 10 Basic Exercises
1.  **Create:** Create a database called `school`.
2.  **Create:** Create a collection named `teachers`.
3.  **Insert:** Insert one teacher document with `name`, `subject`.
4.  **Show:** Show all databases.
5.  **Show:** Show all collections in the `school` database.
6.  **Drop:** Drop the `teachers` collection.
7.  **Insert:** Insert 2 documents into the `students` collection of `college`.
8.  **Read:** Find all documents in `students`.
9.  **Delete:** Delete one student by name.
10. **Count:** Count the total number of students.

#### B. 10 CRUD Exercises
1.  **Insert:** Insert a student named `John`, age 25, city `London`, course `History`.
2.  **InsertMany:** Insert three new students in one query.
3.  **FindOne:** Find the student named `Priya`.
4.  **Find:** Find all students from `Chennai`.
5.  **Update:** Update `John`'s city to `Manchester`.
6.  **UpdateMany:** Increase the marks of all students by 10.
7.  **Delete:** Delete the student named `John`.
8.  **DeleteMany:** Delete all students from `Delhi`.
9.  **Find:** Find and sort all students by name.
10. **Insert with Array:** Insert a new student with `skills: ["C", "Rust"]`.

#### C. 10 Query Exercises
1.  Find students with marks > 90.
2.  Find students with age < 21.
3.  Find students from `Mumbai` or `Delhi`.
4.  Find students with marks between 80 and 90 (inclusive).
5.  Find students who are not from `Chennai`.
6.  Find students whose age is 20 or 22.
7.  Find students with marks less than 80 but age greater than 21.
8.  Find students who know `Python` (using the `skills` array).
9.  Find students from `Chennai` OR with marks > 85.
10. Find students who are from `Mumbai` AND know `Java`.

#### D. 10 Operator Exercises
1.  Find students with `marks` exactly 85 (`$eq`).
2.  Find students with age not equal to 20 (`$ne`).
3.  Find students from `Chennai` or `Mumbai` (`$in`).
4.  Find students not from `Delhi` or `Pune` (`$nin`).
5.  Find students with marks greater than 80 (`$gt`).
6.  Find students with marks greater than or equal to 90 (`$gte`).
7.  Find students with marks less than 80 (`$lt`).
8.  Find students with marks less than or equal to 85 (`$lte`).
9.  Find students with marks > 80 AND age < 22 (`$and`).
10. Find students with marks < 70 OR age > 23 (`$or`).

#### E. 5 Array Exercises
1.  Add `"Angular"` to `Sneha`'s skills (`$push`).
2.  Remove the last skill from `Ravi` (`$pop`).
3.  Remove `"C++"` from `Priya`'s skills (`$pull`).
4.  Add `"MongoDB"` to `Arun`'s skills only if not present (`$addToSet`).
5.  Find all students who have `"React"` in their skills.

#### F. 5 Aggregation Exercises
1.  **Group and Count:** Count the number of students in each city.
2.  **Group and Average:** Find the average age of students in each course.
3.  **Group and Max:** Find the maximum marks for each course.
4.  **Match and Group:** Filter students with marks > 80, then count them by course.
5.  **Projection:** After grouping by course to get the average marks, only show the course and the average.

#### G. 5 Debugging Exercises
*(Find the error in the following)*
1.  `db.students.find(name: "Arun")` (Answer: Missing `{}`, should be `{ name: "Arun" }`).
2.  `db.students.insertOne({ name: "Bob", age: 20, city: "Paris"` (Answer: Missing closing `}`).
3.  `db.students.find({ marks: { $gt } })` (Answer: `$gt` needs a value, e.g., `{ $gt: 80 }`).
4.  `db.students.updateOne({ name: "Arun" }, { city: "Hyderabad" })` (Answer: Missing `$set` operator, should be `{ $set: { city: "Hyderabad" } }`).
5.  `db.students.aggregate({ $match: { city: "Delhi" } })` (Answer: `aggregate()` expects an array, so use `[ { $match: { city: "Delhi" } } ]`).

---

### MODULE 16 – MINI PROJECTS

#### 1. Student Management System
- **Goal:** A system to manage student records.
- **Features:**
    - Add new students.
    - View all students.
    - Update a student's information.
    - Delete a student's record.
    - Search for students by name or course.
    - Display students sorted by marks.
- **Collections:** `students`.

#### 2. Employee Management System
- **Goal:** Manage employee records of a company.
- **Features:**
    - Add employees with details (name, department, salary, joining date).
    - Find all employees in a specific department.
    - Increase salary of all employees in a department by 10%.
    - Delete employees who have left the company.
    - Show employees sorted by salary.
- **Collections:** `employees`.

#### 3. Product Management System
- **Goal:** Manage products in an e-commerce inventory.
- **Features:**
    - Add new products (name, price, category, stock).
    - Find products under a certain price.
    - Update stock after a sale.
    - Find all products in a specific category.
    - Sort products by price (low to high).
- **Collections:** `products`.

#### 4. Library Management System
- **Goal:** Manage books and users.
- **Features:**
    - Add books (title, author, ISBN, availability).
    - Register users.
    - Borrow a book (update availability to false).
    - Return a book (update availability to true).
    - Find all books by a specific author.
- **Collections:** `books`, `users`, `transactions`.

#### 5. Course Management System
- **Goal:** Manage courses and student enrollments.
- **Features:**
    - Add courses (name, description, duration, fee).
    - Add students.
    - Enroll a student in a course (use an embedded document or a separate collection).
    - Find all students enrolled in a course.
    - Find all courses a student is enrolled in.
- **Collections:** `courses`, `students`, `enrollments`.

---

### INTERVIEW PREPARATION: 30 Beginner Questions and Answers

1.  **Q: What is MongoDB?**
    - A: A NoSQL, document-oriented database.
2.  **Q: What is a document in MongoDB?**
    - A: A record in a collection, stored as a JSON-like object.
3.  **Q: What is a collection?**
    - A: A group of documents, like a table in SQL.
4.  **Q: What is BSON?**
    - A: The binary-encoded format MongoDB uses to store data.
5.  **Q: What is the `_id` field?**
    - A: A unique identifier for each document. MongoDB creates it automatically.
6.  **Q: What is NoSQL?**
    - A: Non-relational databases that don't use tables and rows like SQL.
7.  **Q: List 3 advantages of MongoDB.**
    - A: Flexibility, Speed, and Scalability.
8.  **Q: How is MongoDB different from SQL?**
    - A: MongoDB uses collections and documents; SQL uses tables and rows. MongoDB has a dynamic schema; SQL has a fixed schema.
9.  **Q: What is an aggregation pipeline?**
    - A: A framework for data processing where documents pass through a series of stages like `$match`, `$group`, and `$sort`.
10. **Q: What is the difference between `insertOne` and `insertMany`?**
    - A: `insertOne` inserts one document; `insertMany` inserts an array of documents.
11. **Q: What is the difference between `find` and `findOne`?**
    - A: `find` returns all matching documents (a cursor); `findOne` returns the first matching document.
12. **Q: What does `$set` do?**
    - A: It sets or updates the value of a field.
13. **Q: What does `$inc` do?**
    - A: It increments the value of a numeric field.
14. **Q: What does `$push` do?**
    - A: It adds an element to an array.
15. **Q: What does `$pull` do?**
    - A: It removes all occurrences of a value from an array.
16. **Q: What is dot notation used for?**
    - A: To access fields in embedded/nested documents (e.g., `"address.city"`).
17. **Q: What is an index in MongoDB?**
    - A: A data structure that makes queries faster.
18. **Q: How do you create an index?**
    - A: Using `db.collection.createIndex({ field: 1 })`.
19. **Q: What is projection?**
    - A: Selecting which fields to include or exclude in the result.
20. **Q: What does `sort()` do?**
    - A: Orders the results (1 for ascending, -1 for descending).
21. **Q: What does `limit()` do?**
    - A: Limits the number of documents returned.
22. **Q: What is PyMongo?**
    - A: The official Python driver to connect and interact with MongoDB.
23. **Q: What is MongoDB Compass?**
    - A: A graphical user interface (GUI) for MongoDB.
24. **Q: What is MongoDB Atlas?**
    - A: MongoDB's cloud database service.
25. **Q: What is upsert?**
    - A: A combination of update and insert. If the document exists, update it; if not, insert it.
26. **Q: How do you delete a collection?**
    - A: Using `db.collection.drop()`.
27. **Q: How do you delete a database?**
    - A: Using `db.dropDatabase()`.
28. **Q: What does `$group` do in aggregation?**
    - A: Groups documents by a specified field.
29. **Q: What is `mongosh`?**
    - A: The MongoDB command-line shell.
30. **Q: What is a schema?**
    - A: The structure of the data. MongoDB is schema-less or has a dynamic schema, so documents in a collection can have different fields.

---

### CHEAT SHEETS

#### 1. MongoDB Quick Cheat Sheet
| Command | Description |
| :--- | :--- |
| `mongosh` | Open the MongoDB Shell. |
| `show dbs` | List all databases. |
| `use college` | Switch to (or create) the `college` database. |
| `show collections` | List all collections. |
| `db` | Show the current database. |

#### 2. Important Commands
| Command | Description |
| :--- | :--- |
| `db.students.find({})` | Find all documents. |
| `db.students.insertOne({...})` | Insert a document. |
| `db.students.updateOne({...}, {$set:{...}})` | Update a document. |
| `db.students.deleteOne({...})` | Delete a document. |
| `db.students.countDocuments({})` | Count documents. |

#### 3. Important Operators
| Operator | Description | Example |
| :--- | :--- | :--- |
| `$gt` | Greater Than | `{marks: {$gt: 80}}` |
| `$lt` | Less Than | `{age: {$lt: 20}}` |
| `$gte` | Greater Than or Equal | `{marks: {$gte: 85}}` |
| `$lte` | Less Than or Equal | `{age: {$lte: 21}}` |
| `$eq` | Equal To | `{city: {$eq: "Chennai"}}` |
| `$ne` | Not Equal To | `{course: {$ne: "Python"}}` |
| `$in` | In an array | `{city: {$in: ["Mumbai", "Delhi"]}}` |
| `$nin` | Not in an array | `{course: {$nin: ["Java", "C++"]}}` |
| `$and` | Logical AND | `{$and: [{age: 20}, {city: "Chennai"}]}` |
| `$or` | Logical OR | `{$or: [{age: 20}, {city: "Chennai"}]}` |
| `$set` | Set field value | `{$set: {city: "Pune"}}` |
| `$inc` | Increment value | `{$inc: {marks: 5}}` |
| `$push` | Add to array | `{$push: {skills: "HTML"}}` |
| `$pull` | Remove from array | `{$pull: {skills: "SQL"}}` |

#### 4. CRUD Cheat Sheet
| Operation | MongoDB Query |
| :--- | :--- |
| **CREATE** | |
| Insert One | `db.students.insertOne({...})` |
| Insert Many | `db.students.insertMany([{...}, {...}])` |
| **READ** | |
| Find All | `db.students.find({})` |
| Find One | `db.students.findOne({name: "Arun"})` |
| **UPDATE** | |
| Update One | `db.students.updateOne({name: "Arun"}, {$set: {age: 21}})` |
| Update Many | `db.students.updateMany({city: "Delhi"}, {$set: {city: "New Delhi"}})` |
| **DELETE** | |
| Delete One | `db.students.deleteOne({name: "Arun"})` |
| Delete Many | `db.students.deleteMany({city: "Delhi"})` |

#### 5. Aggregation Cheat Sheet
| Stage | Description | Example |
| :--- | :--- | :--- |
| `$match` | Filters documents. | `{ $match: { marks: { $gt: 80 } } }` |
| `$group` | Groups documents. | `{ $group: { _id: "$course", total: { $sum: 1 } } }` |
| `$sort` | Sorts documents. | `{ $sort: { total: -1 } }` |
| `$project` | Shapes the output. | `{ $project: { course: "$_id", _id: 0 } }` |
| `$limit` | Limits the output. | `{ $limit: 2 }` |
| `$sum` | Aggregator (used in `$group`). | `{ $sum: 1 }` or `{ $sum: "$marks" }` |
| `$avg` | Aggregator (used in `$group`). | `{ $avg: "$marks" }` |

#### 6. Common Beginner Mistakes
- **Forgetting `{}`:** `find()` always needs a query object, even if empty `{}`.
- **Missing `$` in operators:** Forgetting the `$` in `$set`, `$gt`, etc.
- **String vs. Number:** `{age: "20"}` is a string; `{age: 20}` is a number. They are different!
- **Using `$` for fields:** Only use `$` for field names in `aggregation` or `update` operators.
- **Ignoring `_id`:** The `_id` field is immutable once set. You can't change it.
- **Not using projections:** Fetching all fields when you only need one is inefficient.

#### 7. Final Practice Test
1.  Create a database `library`.
2.  Create a collection `books`.
3.  Insert the following books:
    - `{ title: "The Hobbit", author: "J.R.R. Tolkien", genre: "Fantasy", pages: 310 }`
    - `{ title: "1984", author: "George Orwell", genre: "Dystopian", pages: 328 }`
    - `{ title: "Dune", author: "Frank Herbert", genre: "Sci-Fi", pages: 412 }`
4.  Find all books.
5.  Find the book titled "1984".
6.  Find all books with more than 320 pages.
7.  Find all books in the "Fantasy" genre.
8.  Update "Dune" to have 500 pages.
9.  Delete "1984".
10. Count all books in the collection.

#### 8. Mini Project Assignment
- **Project:** **Student Management System**
- **Deadline:** End of the week.
- **Deliverables:** A Python script that uses PyMongo to perform the following tasks:
    1.  Connect to a local MongoDB database.
    2.  Allow the user to choose an option from a menu:
        - Add a new student (name, age, course, marks).
        - View all students.
        - Update a student's marks (by name).
        - Delete a student (by name).
        - Find students with marks greater than a specified value.
        - Exit the program.
    3.  Use appropriate CRUD operations.
    4.  Handle potential errors (e.g., student not found).